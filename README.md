# Jarkom-Modul-3-B03-2022

## Anggota Kelompok:

| Nama                           | NRP        |
| ------------------------------ | ---------- |
| Maheswara Danendra Satriananda | 5025201060 |
| James Silaban                  | 5025201169 |
| Anak Agung Yatestha Parwata    | 5025201234 |

1. Loid bersama Franky berencana membuat peta tersebut dengan kriteria WISE sebagai DNS Server, Westalis sebagai DHCP Server, Berlint sebagai Proxy Server

| Ostania          | <p>auto eth0</p><p>iface eth0 inet dhcp</p><p></p><p>auto eth1</p><p>iface eth1 inet static</p><p>` `address 192.174.1.1</p><p>` `netmask 255.255.255.0</p><p></p><p>auto eth2</p><p>iface eth2 inet static</p><p>` `address 192.174.2.1</p><p>` `netmask 255.255.255.0</p><p></p><p>auto eth3</p><p>iface eth3 inet static</p><p>` `address 192.174.3.1</p><p>` `netmask 255.255.255.0</p> |
| :--------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Konfigurasi WISE | <p>auto eth0</p><p>iface eth0 inet static</p><p>` `address 192.174.2.2</p><p>` `netmask 255.255.255.0</p><p>` `gateway 192.174.2.1</p>                                                                                                                                                                                                                                                      |
| Berlint          | <p>auto eth0</p><p>iface eth0 inet static</p><p>` `address 192.174.2.3</p><p>` `netmask 255.255.255.0</p><p>` `gateway 192.174.2.1</p>                                                                                                                                                                                                                                                      |
| Westalis         | <p>auto eth0</p><p>iface eth0 inet static</p><p>` `address 192.174.2.4</p><p>` `netmask 255.255.255.0</p><p>` `gateway 192.174.2.1</p>                                                                                                                                                                                                                                                      |
| Eden             | <p>auto eth0</p><p>iface eth0 inet static</p><p>` `address 192.174.3.2</p><p>` `netmask 255.255.255.0</p><p>` `gateway 192.174.3.1</p>                                                                                                                                                                                                                                                      |
| NewstonCastle    | <p>auto eth0</p><p>iface eth0 inet static</p><p>` `address 192.174.3.3</p><p>` `netmask 255.255.255.0</p><p>` `gateway 192.174.3.1</p>                                                                                                                                                                                                                                                      |
| KemonoPark       | <p>auto eth0</p><p>iface eth0 inet static</p><p>` `address 192.174.3.4</p><p>` `netmask 255.255.255.0</p><p>` `gateway 192.174.3.1</p>                                                                                                                                                                                                                                                      |
| SSS              | <p>auto eth0</p><p>iface eth0 inet static</p><p>` `address 192.174.1.2</p><p>` `netmask 255.255.255.0</p><p>` `gateway 192.174.1.1</p>                                                                                                                                                                                                                                                      |
| Garden           | <p>auto eth0</p><p>iface eth0 inet static</p><p>` `address 192.174.1.3</p><p>` `netmask 255.255.255.0</p><p>` `gateway 192.174.1.1</p>                                                                                                                                                                                                                                                      |

| <p>Wise DNS Server </p><p>(scriptWise.sh)</p>               | <p>apt-get update</p><p>apt-get install bind9 -y</p>                         |
| :---------------------------------------------------------- | :--------------------------------------------------------------------------- |
| <p>Westalis DHCP Server</p><p>(scriptWestalis.sh)</p>       | <p>apt-get update</p><p>apt-get install isc-dhcp-server -y</p><p></p><p></p> |
| <p>Berlint Proxy Server</p><p>(scriptBerlint.sh)</p><p></p> | <p>apt-get update</p><p>apt-get install squid -y</p>                         |

1. Ostania sebagai DHCP Relay

| <p>Ostania DHCP Relay</p><p>(script.sh)</p> | apt-get update<br>apt-get install isc-dhcp-relay -y<br><br>Kemudian edit file /etc/default/isc-dhcp-relay dengan menambahkan SERVER = "192.174.2.4" dan INTERFACES = "eth1 eth2 eth3"<br><br>service isc-dhcp-relay restart |
| :------------------------------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

![](https://user-images.githubusercontent.com/70903245/201679105-0d1f4076-7d74-465a-83f9-bb12376c4791.png)

1. Client yang melalui Switch1 mendapatkan range IP dari [prefix IP].1.50 - [prefix IP].1.88 dan [prefix IP].1.120 - [prefix IP].1.155

| <p>Konfigurasi Westalis</p><p>(tambahan di script.sh)</p> | <p>echo ‘</p><p>INTERFACES=”eth0”</p><p>‘ > /etc/default/isc-dhcp-server</p><p></p><p>echo ‘</p><p>subnet 192.174.1.0 netmask 255.255.255.0 {</p><p>` `range 192.174.1.50 192.174.1.88;</p><p>` `range 192.174.1.120 192.174.1.155;</p><p>` `option routers 192.174.1.1;</p><p>` `option broadcast-address 192.174.1.255;</p><p>` `option domain-name-servers 192.174.2.2;</p><p>` `default-lease-time 300;</p><p>` `max-lease-time 6900;</p><p>}</p><p>subnet 192.174.2.0 netmask 255.255.255.0{</p><p>}</p><p></p><p>‘ > /etc/dhcp/dhcpd.conf</p><p>service isc-dhcp-server restart</p><p>service isc-dhcp-server status</p> |
| :-------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| <p>SSS</p><p>(scriptSSS.sh)</p><p></p>       | <p>echo '</p><p>#auto eth0</p><p>#iface eth0 inet static</p><p># address 192.174.1.2</p><p># netmask 255.255.255.0</p><p># gateway 192.174.1.1</p><p>auto eth0</p><p>iface eth0 inet dhcp</p><p>' > /etc/network/interfaces</p> |
| :------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>Garden</p><p>script(Garden.sh)</p><p></p> | <p>echo '</p><p>#auto eth0</p><p>#iface eth0 inet static</p><p># address 192.174.1.3</p><p># netmask 255.255.255.0</p><p># gateway 192.174.1.1</p><p>auto eth0</p><p>iface eth0 inet dhcp</p><p>' > /etc/network/interfaces</p> |

1. Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.10 - [prefix IP].3.30 dan [prefix IP].3.60 - [prefix IP].3.85

| <p>Konfigurasi Westalis</p><p>(tambahan di scriptWestalis.sh)</p> | <p>echo ‘</p><p>subnet 192.174.3.0 netmask 255.255.255.0 {</p><p>` `range 192.174.3.10 192.174.3.30;</p><p>` `range 192.174.3.60 192.174.3.85;</p><p>` `option routers 192.174.3.1;</p><p>` `option broadcast-address 192.174.3.255;</p><p>` `option domain-name-servers 192.174.2.2;</p><p>` `default-lease-time 600;</p><p>` `max-lease-time 6900;</p><p>}</p><p>‘ >> /etc/dhcp/dhcpd.conf</p><p>service isc-dhcp-server restart</p> |
| :---------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| <p>Eden</p><p>(scriptEden.sh)</p><p></p>             | <p>echo '</p><p>#auto eth0</p><p>#iface eth0 inet static</p><p># address 192.174.3.2</p><p># netmask 255.255.255.0</p><p># gateway 192.174.3.1</p><p>auto eth0</p><p>iface eth0 inet dhcp</p><p>' > /etc/network/interfaces</p> |
| :--------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>NewstonCastle</p><p>(scriptNewston.sh)</p><p></p> | <p>echo '</p><p>#auto eth0</p><p>#iface eth0 inet static</p><p># address 192.174.3.3</p><p># netmask 255.255.255.0</p><p># gateway 192.174.3.1</p><p>auto eth0</p><p>iface eth0 inet dhcp</p><p>' > /etc/network/interfaces</p> |
| <p>KemonoPark</p><p>(scriptKemono.sh)</p><p></p>     | <p>echo '</p><p>#auto eth0</p><p>#iface eth0 inet static</p><p># address 192.174.3.4</p><p># netmask 255.255.255.0</p><p># gateway 192.174.3.1</p><p>auto eth0</p><p>iface eth0 inet dhcp</p><p>' > /etc/network/interfaces</p> |

1. Client mendapatkan DNS dari WISE dan client dapat terhubung dengan internet melalui DNS tersebut

| WISE (scriptWise2.sh)                        | <p>echo '</p><p>options {</p><p>` `directory "/var/cache/bind";</p><p>` `forwarders {</p><p>` `192.168.122.1;</p><p>` `};</p><p>` `allow-query{any;};</p><p>` `auth-nxdomain no; # conform to RFC1035</p><p>` `listen-on-v6 { any; };</p><p>};</p><p>' > /etc/bind/named.conf.options</p><p></p><p>service bind9 restart</p> |
| :------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Westalis                                     | <p>jalankan command</p><p>service isc-dhcp-server restart</p>                                                                                                                                                                                                                                                                |
| Ostania                                      | <p>jalankan command </p><p>service isc-dhcp-relay restart</p>                                                                                                                                                                                                                                                                |
| SSS, Garden, Eden, NewstonCastle, KemonoPark | <p>gausa di matikan, langsung aja jalankan command</p><p>cat /etc/resolv.conf</p>                                                                                                                                                                                                                                            |

![A screenshot of a computer

Description automatically generated with medium confidence](https://user-images.githubusercontent.com/70903245/201679108-e5a95aa3-af77-4002-b4d9-a921e95892cf.png)

![Text

Description automatically generated](https://user-images.githubusercontent.com/70903245/201679078-ce739bf0-a650-4d07-b70e-5390b93b935a.png)

![Text

Description automatically generated](https://user-images.githubusercontent.com/70903245/201679091-59882134-c298-4f60-865b-7d8bb58cdc0a.png)

![Text

Description automatically generated](https://user-images.githubusercontent.com/70903245/201679093-b680bae3-4566-4214-b124-16eef3b222d7.png)

![Text

Description automatically generated](https://user-images.githubusercontent.com/70903245/201679097-92ea21d5-a276-4231-863d-aaf5897cada9.png)

1. Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch1 selama 5 menit sedangkan pada client yang melalui Switch3 selama 10 menit. Dengan waktu maksimal yang dialokasikan untuk peminjaman alamat IP selama 115 menit.
1. Loid dan Franky berencana menjadikan Eden sebagai server untuk pertukaran informasi dengan alamat IP yang tetap dengan IP [prefix IP].3.13

| <p>Eden</p><p></p>                                                                               | <p>Cek ip a nya</p><p></p>                                                                                                                                                                                  |
| :----------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Westalis</p><p>(scriptWestalis2.sh)</p>                                                       | <p>echo '</p><p>host Eden {</p><p>` `hardware ethernet 9e:ec:fd:62:79:4e;</p><p>` `fixed-address 192.174.3.13;</p><p>` `}</p><p>' >> /etc/dhcp/dhcpd.conf </p><p>service isc-dhcp-server restart</p><p></p> |
| Ostania                                                                                          | <p>jalankan command</p><p>service isc-dhcp-relay restart</p>                                                                                                                                                |
| <p>Eden</p><p>(scriptEden2.sh)</p>                                                               | <p>echo '</p><p>` `hwaddress ether 9e:ec:fd:62:79:4e</p><p>' >> /etc/network/interfaces</p><p></p>                                                                                                          |
| Matikan Node Eden dan Nyalakan Ulang untuk melihat apakah IP ke 192.174.3.13 berhasil ditetapkan |                                                                                                                                                                                                             |

# PROXY

No 1

| <p>Berlint</p><p>proxy1.sh</p> | <p>apt-get install squid</p><p>mv /etc/squid/squid.conf /etc/squid/squid.conf.bak</p><p></p><p>echo '</p><p>acl WORKING time MTWHF 08:00-17:00d</p><p>' > /etc/squid/acl.conf</p><p></p><p>echo '</p><p>include /etc/squid/acl.conf</p><p></p><p>http_port 8080</p><p>visible_hostname Berlint</p><p></p><p>http_access deny WORKING</p><p>http_access allow all</p><p>' > /etc/squid/squid.conf</p><p></p><p>service squid restart</p><p></p> |
| :----------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>SSS</p><p>testing</p>       | <p>export http_proxy=”[http://192.174.2.3:8080](http://192.175.2.3:8080)”</p><p></p><p>date -s “7 nov 2022 13:00”</p><p>lynx google.com</p><p></p><p>date -s “7 nov 2022 18:00”</p><p>lynx google.com</p>                                                                                                                                                                                                                                      |

No 2

| <p>Berlint</p><p>proxy2.sh</p> | <p>echo '</p><p>loid-work.com</p><p>franky-work.com</p><p>' > /etc/squid/work-sites.acl</p><p></p><p>echo '</p><p>include /etc/squid/acl.conf</p><p></p><p>http_port 8080</p><p>visible_hostname Berlint</p><p></p><p>acl WORKSITES dstdomain "/etc/squid/work-sites.acl"</p><p>http_access allow WORKSITES</p><p>http_access deny WORKING</p><p>http_access allow all</p><p>' > /etc/squid/squid.conf</p><p></p><p>service squid restart</p><p></p> |
| :----------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>SSS</p><p>testing</p>       | <p>export http_proxy=”[http://192.174.2.3:8080](http://192.175.2.3:8080)”</p><p></p><p>date -s “7 nov 2022 13:00”</p><p>lynx google.com</p><p>lynx loid-work.com</p><p>lynx franky-work.com</p>                                                                                                                                                                                                                                                      |

no 3

| <p>Berlint</p><p>proxy3.sh</p> | <p>echo '</p><p>include /etc/squid/acl.conf</p><p></p><p>http_port 8080</p><p>visible_hostname Berlint</p><p></p><p>acl SSL_ports port 443</p><p>acl WORKSITES dstdomain "/etc/squid/work-sites.acl"</p><p>http_access deny !SSL_ports</p><p>http_access allow WORKSITES</p><p>http_access deny WORKING</p><p>http_access allow all</p><p>' > /etc/squid/squid.conf</p><p></p><p>service squid restart</p> |
| :----------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>SSS</p><p>testing</p>       | <p>export http_proxy=”[http://192.174.2.3:8080](http://192.175.2.3:8080)”</p><p></p><p>date -s “7 nov 2022 18:00”</p><p>lynx <http://example.com></p><p>lynx <https://example.com></p><p></p>                                                                                                                                                                                                              |

no 4

| <p>Berlint</p><p>(proxy4.sh)</p><p>- http_access deny !SSL_ports<br> dimatikan karena speedtest menggunakan HTTP # http_access deny WORKING</p> | <p>echo ' </p><p></p><p>include /etc/squid/acl.conf</p><p></p><p>http_port 8080</p><p>visible_hostname Berlint</p><p></p><p>acl SSL_ports port 443</p><p>acl WORKSITES dstdomain "/etc/squid/work-sites.acl"</p><p># http_access deny !SSL_ports</p><p>http_access allow WORKSITES</p><p># http_access deny WORKING</p><p>http_access allow all</p><p></p><p>delay_pools 1</p><p>delay_class 1 2</p><p>delay_access 1 allow all</p><p>delay_parameters 1 none 16000/16000</p><p>'  > /etc/squid/squid.conf</p> |
| :---------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>SSS & Garden</p><p>(testing)</p>                                                                                                             | <p>unset http_proxy</p><p></p><p>apt install speedtest-cli</p><p></p><p>export PYTHONHTTPSVERIFY=0</p><p>export http_proxy="[http://192.174.2.3:8080](http://192.175.2.3:8080)"</p><p></p><p>date -s "12 nov 2022 19:00" #sesuaikan</p><p>speedtest</p>                                                                                                                                                                                                                                                        |

![](https://user-images.githubusercontent.com/70903245/201678463-9cb1b505-edd0-47ce-8488-5e23fbe89010.png)

no 5

| <p>Berlint</p><p>(proxy5.sh)</p><p><br></p><p>- http_access deny !SSL_ports<br> dimatikan karena speedtest menggunakan HTTP</p> | <p>echo ' </p><p></p><p>include /etc/squid/acl.conf</p><p></p><p>http_port 8080</p><p>visible_hostname Berlint</p><p></p><p>acl SSL_ports port 443</p><p>acl WORKSITES dstdomain "/etc/squid/work-sites.acl"</p><p># http_access deny !SSL_ports</p><p>http_access allow WORKSITES</p><p># http_access deny WORKING</p><p>http_access allow all</p><p></p><p>acl OPEN_TIME time MTWHF</p><p>delay_pools 1</p><p>delay_class 1 2</p><p>delay_access 1 allow !OPEN_TIME</p><p>delay_parameters 1 none 16000/16000</p><p>'  > /etc/squid/squid.conf</p> |
| :------------------------------------------------------------------------------------------------------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>SSS & Garden</p><p>(testing)</p>                                                                                             | <p>unset http_proxy</p><p></p><p>apt install speedtest-cli</p><p></p><p>export PYTHONHTTPSVERIFY=0</p><p>export http_proxy="[http://192.174.2.3:8080](http://192.175.2.3:8080)"</p><p></p><p>date -s "12 nov 2022 19:00" #sesuaikan</p><p>speedtest</p>                                                                                                                                                                                                                                                                                              |

#testing terakhir sesuai tabel

| <p>Berlint</p><p>(proxyTest.sh)</p><p><br></p><p>- ` `http_access deny !SSL_ports<br> dimatikan karena speedtest menggunakan HTTP</p> | <p>echo ' </p><p></p><p>include /etc/squid/acl.conf</p><p></p><p>http_port 8080</p><p>visible_hostname Berlint</p><p></p><p>acl SSL_ports port 443</p><p>acl WORKSITES dstdomain "/etc/squid/work-sites.acl"</p><p>http_access deny !SSL_ports</p><p>http_access allow WORKSITES</p><p>http_access deny WORKING</p><p>http_access allow all</p><p></p><p>acl OPEN_TIME time MTWHF</p><p>delay_pools 1</p><p>delay_class 1 2</p><p>delay_access 1 allow !OPEN_TIME</p><p>delay_parameters 1 none 16000/16000</p><p>'  > /etc/squid/squid.conf</p><p></p><p>service squid restart</p> |
| :------------------------------------------------------------------------------------------------------------------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>SSS & Garden</p><p>(testing)</p>                                                                                                   | <p>unset http_proxy</p><p></p><p>apt install speedtest-cli</p><p></p><p>export PYTHONHTTPSVERIFY=0</p><p>export http_proxy="[http://192.174.2.3:8080](http://192.175.2.3:8080)"</p><p></p><p>date -s "12 nov 2022 19:00" #sesuaikan</p><p>speedtest</p>                                                                                                                                                                                                                                                                                                                             |

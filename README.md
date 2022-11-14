# Jarkom-Modul-3-B03-2022

## Anggota Kelompok:

| Nama                           | NRP        |
| ------------------------------ | ---------- |
| Maheswara Danendra Satriananda | 5025201060 |
| James Silaban                  | 5025201169 |
| Anak Agung Yatestha Parwata    | 5025201234 |

PROXY

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

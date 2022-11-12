# Jarkom-Modul-3-ITA09-2022

(1&2)  Loid bersama Franky berencana membuat peta tersebut dengan kriteria WISE sebagai DNS Server, Westalis sebagai DHCP Server, Berlint sebagai Proxy Server. Dan Ostania sebagai DHCP Relay.

Bentuk topologi: 

![](https://lh5.googleusercontent.com/yp4zZrp3ROKWHb06a7dmgksgjBs4Jp1b0NTBJt81ur6kezKsYs9im3Nry5E8XzGdn4p7ElHIxm-URLUp_SuLahFx7RbM5XfGZFqiBFFg30EPx6OQ_MaPRT0QNPkwDCRsRM0WiWxeUxhVmq53PtQR2pgreLy66NcyBCNPOXaDDP97EaJIGVVCX5G3OKyMIA)

Command yang akan dijalankan pada node ostania adalah: 

![](https://lh4.googleusercontent.com/NYCKHD4m4g1-yvN7CUg79e_Wc6MLQf9wov-EgXECJ0W1bfUlASgSaCy_uos024c9rk4w1hxeiFddsr0i2OfgpklpfH1_ZoFlZJEph_MatJFy6fXnJl77xjX7p5RQazo5TatWXFe_pi2bFbGn4RxkzuXQ0I7Y4Lo751U_gLD-SfAYo1jZEEPv1pt35FQKhg)

Lalu saat install isc-dhcp-relay kita manjadikan Westalis dengan IP 10.44.2.4 sebagai dhcp-server dan interface akan kita buat listen pada eth1 eth2 dan eth3

![](https://lh3.googleusercontent.com/293-xwz6ZrkguNhZwA3_RBk6n_0Olbh9pt6xlxNlpqjeqN2pwkAR1T0gnWRGljAiAE9bIsud1CBZHhoDIuTSI41nxKZrtMJHW5107TyXbP9SVlz217D5-Z-gKkxmZnw0i1oSzmXiAl-ltRYd5wbIxQN33dzJFyslwuCWt6Vx4HroWoBtjO3kCQpwhsI18g)

Ada beberapa kriteria yang ingin dibuat oleh Loid dan Franky, yaitu:

1.  Semua client yang ada HARUS menggunakan konfigurasi IP dari DHCP Server.

2.  Client yang melalui Switch1 mendapatkan range IP dari [prefix IP].1.50 - [prefix IP].1.88 dan [prefix IP].1.120 - [prefix IP].1.155 (3)

3.  Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.10 - [prefix IP].3.30 dan [prefix IP].3.60 - [prefix IP].3.85 (4)

4.  Client mendapatkan DNS dari WISE dan client dapat terhubung dengan internet melalui DNS tersebut. (5)

5.  Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch1 selama 5 menit sedangkan pada client yang melalui Switch3 selama 10 menit. Dengan waktu maksimal yang dialokasikan untuk peminjaman alamat IP selama 115 menit. (6)

Westalis

Pertama kita akan membuat nameserver 192.168.122.1 sehingga westalis dapat terhubung ke internet dan mendownload isc-dhcp-relay

![](https://lh4.googleusercontent.com/_eDeHrtDAcUIPsePg6Lk9z9RYPxS_4Qg5CtmnjaA-2b5PSK7B98XtjlwnCGKgmqGi54stNLjxLBPxF4_naWOwm7-3gw0ySkNuIpk_2zAcjgPmKgA8-l9CM5SLSx3sEqIClHGBJZiTFTdwpLtfHeUssX7qomnKw8KL7Z62qDeET83dMcWOMn1n1uqPbF7ew)

Lalu, kita tambahkan interface eth0 pada /etc/default/isc-dhcp-server

![](https://lh6.googleusercontent.com/iqq0_ij8GLaR-8oGWf_0S2HqCnKq1nWGWhsIFI0iqbDqHYMkNNCAWaAU3LsLiPM8j1llhPZF85MmXUQtiFOj2q11ulylRE3_mUFY-s4Mi5IJBKEBiVlwqahpNyHaila_LwIxT2pTdcF1KXzKYYKCD0flUd5IZS92KYoCvS-XgKONvlNe2A5oYZS8h1Ch0A)

Pertama Kita akan menjalankan relay dengan konfig pada /etc/dhcp/dhcpd.conf

![](https://lh5.googleusercontent.com/vn8XKfbO-xJaxD1JRmyhbLn6wuAq19NnJXW4F14eJPNTQNoUszJ6XYR9Jd7wT2HEmiSMScBP0_LQCFnRhB70RdzLYrB0S81jr8EuNgdx5F87oY_lkaV3-M13VpDqOXA_QZdipjSB476yu_2G2wB_bJ6oLr9T_S_FT8dbatkg3bnS641zBicX8WdrRbPFZw)

Selanjutnya kita akan setting pada switch1 dengan menambahkan konfig dibawah pada /etc/dhcp/dhcpd.conf

![](https://lh3.googleusercontent.com/7KMLpqrijFRM5EQQd3aiTIwqYpOBRocEswutaMqj2RCQkbPO0Uc6qQ85s9DQstjTGBlyPDnaBbvjRxfc4DREJF2AlUf6Kuzh1ysUwTISAg50mhxK9ysyNeWD92quxq-aY_ZTCBfi8e4TtOX0nf6NbDZYUMm6RvYE24ZfvWCYE4i8mtW8Ymj-_7dbqTr-DQ)d

disini, untuk range sudah diatur sesuai dengan ketentuan soal. Lalu, untuk DNS sudah diarahkan ke IP WISE 10.44.2.2 dan untuk waktu meminjam alamat IP ke client adalah 5 menit atau 300 detik dengan waktu maksimal adalah 115 menit atau 6900 detik.

Selanjutnya kita akan setting switch3 dengan menambahkan konfig sebagai berikut:

![](https://lh5.googleusercontent.com/fQOarqCB4XaVd-muWTfy6ScXoR1ABN17_S77hHylD_nJuM8rbwGhSUqOzKdbbklMe2UOVzfa-_wi0avUUlgIJ3zFJIWI_aVlySkOkaTbqahvTh9L0i4w_xbaoekbIOu7pmLrbUjUrfVXWslBzkABLuuuDG4Eogye8xuCmWO-SIIwXOtcWMkqO_AIZRKUtA)

range sudah diatur sesuai dengan ketentuan soal. Lalu, untuk DNS sudah diarahkan ke IP WISE 10.44.2.2 dan untuk waktu meminjam alamat IP ke client adalah 10 menit atau 600 detik dengan waktu maksimal adalah 115 menit atau 6900 detik.

Client

Kita akan menerapkan settingan DHCP pada client dengan merubah settingan pada /etc/network/interfaces seluruh client menjadi seperti berikut:

![](https://lh6.googleusercontent.com/8LUrGh3q0nNWk9FLpa1hx8DHm1of11yWCp_0uTju1Ag7tqxMrsTPy9I2WmP0iUiI58xaZXlBu5j_G17XFu4mYQ4PsAC12Du_8otbakk7Zv-p1EvdMTEo93kzzrxrPSPp5tOtisd1Kni9hp4N556Rc4PaME2Ekqf7Mh_bqj5TqkxpU-4MnCDdz1AmiHChSA)

Wise

Kita akan membuat seluruh client dapat mengakses internet, kita akan mengkonfig Wise

terlebih dahulu:

![](https://lh4.googleusercontent.com/x85a-yuP2za63JfiQZtFn7qyrmL6ButhQCAJIODajrSLMWR3Pc-4QoalfmG6zpau0o0UvgY9IPba09mnnlHQuTXCS36FlaldydyRnmNaqFjDoiCe7H_qObKarHl-TU2abpIdhuMOG__FFG0Ebr89diS6E3D32pGGwKpFfF-S77MAwF69djkqyGz3e2OAfQ)

Kita akan membuat DNS forwarder pada wise dengan membuat node wise dapat mengakses internet dengan menambahkan nameserver yang sama dengan nameserver Ostania. Lalu, setelah berhasil install bind9 dan lynx kita akan mengkonfig pada /etc/bind/named.conf.options menjadi seperti berikut:

![](https://lh5.googleusercontent.com/ZEn6AXQ1tAXgMwyqHlfHlTajXQBxK4ZcQQbvSHatz7-gi7QhHzY5hsCCkoRhsvgytNlu_4KUqwOD2PKYYBodYUEkjpoDMjMaI2tMaDqebyJ-wLCVGZAfgKBBKjnJuL_i8sNLVrZxFd6dJEDoP32amSJ490bZ1mXQSd6pnnQ1mwbRO5rAwSfwxkTzEnlBYg)

Testing

SSS

![](https://lh5.googleusercontent.com/n_Eb2jI8cT9dwRHZ-rlALTog8B9r_xs-qW5Hu0Q_irowdqALFI41ufwiVZUcQk28MM_zRK6ktDWqCtQkI2XsSpEoLaJq4WfGMp3ShT2QKDdEO8ZFRReArVI2NzOEZ1gUbI5rRWut0s6xq8IBgQLOJGUu5-lu_3yyFcBvNT0_PHCQJGMhTXB7HXWznpa9NA)

Garden

![](https://lh6.googleusercontent.com/pbcZQ0GQP8tpekNOh0Wb9D2CNXqNKE_sSl9FbjkQx2SAJ91TWHXp1etRevQL7Yci6F0VliIFQVcMDRs6KktKZxgRIBCIcbpfx9Lg7cKgOOA1TSNcKtJf4rklSkrNG0GoiM0_zkwvyxhzf5-_23qJvlMfXsG1PQVsoEJnrcbgHKTP-vJQTexpZdSvoEVIdg)

KemonoPark

![](https://lh3.googleusercontent.com/bAoyM8isTpmlGD_Om_KnOqU6HTLzXsD_8VYvcHRcBCFY-AkIkHywFwdITvMjej3Gw8U5TxgLrE2kXcMQdim5F6qe33EZagQuIYRAZhIsahdR07JLY6cgcHhz3-yASzbM89GW5GEBWBK8gQgF9XA_1tJI2GkWKmS5hJ7R7rmWoq5vmfTRQElO2GVxyT14Hw)

NewstonCastle

![](https://lh4.googleusercontent.com/bdrstAHK4tCTfLuOrRvJP-l1NbxmW4qId0Qsd_nLDG0QSEXYkXkj6QxOwTkjv-E1SjfzpNxF5cTebnw7bYvgoIpgBtisPNjkemiqMJZpjqgjLcZrrR38lA94bP69pq_3LFDoXqcQc65KKUZ7LSgYqOx9uOaKZOnLxfyx_pYXxdZliu8EfKXldV0qn1pKRw)

Pada hasil testing diatas dapat terlihat bahwa setiap dhcp client mendapatkan ip yang sesuai dengan range yang telah dibagikan oleh dhcp server dan mendapatkan akses internet lewat dns server dengan ip 10.44.2.2

Loid dan Franky berencana menjadikan Eden sebagai server untuk pertukaran informasi dengan alamat IP yang tetap dengan IP [prefix IP].3.13 (7).

Pertama dengan command ip a di node Eden kita dapat melihat hwaddress pada Eden

![](https://lh6.googleusercontent.com/_PnUeOD1E0R-tthnVI2ndbxLjK8UJF58IBvTKbMUm4qtRqhi2BA7Ycstj5NQfxXMe4T17eIxY7bNJg4ovDmBn1gHdX8zqcDEeecy6U7TbJu5QxukPrdApYe1CpcLPlpqSHns88aTdbknIl9lCY9AzoICngOOi_BuMG_6hi3gVH36FeiNy0wGihsA4If1XA)

Lalu kita ganti network interface eden menjadi berikut:

![](https://lh3.googleusercontent.com/fD_LMB3x6OASVsc-cvX4SZxBgS17J60VRYaaY_TV36ECJIpEH-u-lPGPaff7YADZesLIzStcH-PkMReV9WV9UcgIFK7ucaKA9fWrK6xxMvzr9Y89cu4PSHZITjRDwhRzR_6zngnTvsaIc6WLde74mvgPPJMSieGZxQpa4B5JyApjSNRU8_9jAgDJrB7R5w)

Pada Westalis, kita tambahkan host Eden pada /etc/dhcp/dhcpd.conf yang fixed-address dan hwaddress telah diatur

![](https://lh3.googleusercontent.com/N4d1ltJ5M6Ihb5-OMVAJKu635KdloChBeC2HdCiufAOqviND4OniZSHSYJWFr7Uw3VacRWCT0isqkTjqUDDUmfpqFE0fEXWHHkLpiKdhFiBRhbZcf4Dev9S9MPyCyj8a-c2x7V98wtB8QlUEPXhza63xvzTaF4nxWLGHcq9tLD9fCjOAsSskblTke1Wptw)

Testing

![](https://lh4.googleusercontent.com/bE4QeUfoEN5cqPTkMlHvs89rwTOimVaSVSgo9iwrDio4yQxO2Xo9u24ZYvqjCj9wzE9FA8ufonnmmhUms2Gj6kPJFrxCcKemW2es6XlD0YwP2aPX5nF0azQtP9bQkdpV9SIKz59n4BFtQKdqmirsVSJerrXWP7KY8xi3jLNWPiP3iAYl9JtbPSGun7Hd8A)

Pada hasil testing diatas, Eden telah berhasil mendapatkan fixed ip address yang telah ditentukan sebelumnya.

SSS, Garden, dan Eden digunakan sebagai client Proxy agar pertukaran informasi dapat terjamin keamanannya, juga untuk mencegah kebocoran data.

Pada Proxy Server di Berlint, Loid berencana untuk mengatur bagaimana Client dapat mengakses internet. Artinya setiap client harus menggunakan Berlint sebagai HTTP & HTTPS proxy. Adapun kriteria pengaturannya adalah sebagai berikut:

Disini kita setup agar Berlint berlaku sebagai Proxy Server dengan melakukan konfigurasi sesuai dengan contoh. Pertama kita lakukan instalasi squid di Berlint. Kemudian kita restart berlint dengan menyalakan dan mematikan node. Disana kita lakukan cek status berjalan atau tidak dengan service squid status

![](https://lh5.googleusercontent.com/h4iM2zL-iRJL_p4Tyl9jlsn4kM4CVDJogteAhatOjDhbh2LHW_XRWsW0ljR2ZF8BbTdUBxuzvSnV5LMrQnjqnVKEwlvwl3tkCkWh_NZI3njGkb6xMUe-hUEJWDqrRaDe5v-Vv5t_HYQNlevtVCLx_Tg2Cdk6vtUhiTOg64NkPTRBa6fIC3e_v5vSQ2v_-A)

Setelah itu lakukan konfigurasi Squid dengan backup file konfigurasi, buat file konfigurasi baru di /etc/squid/squid.conf, dan masukkan script yang sesuai di modul. Jika sudah, lakukan restart service squid. Jika statusnya ok, coba di client.

Karena SSS, Garden, dan Eden digunakan sebagai client Proxy, aktifkan proxy dengan 

export http_proxy="[http://ip-proxy-server:port](about:blank)", dengan ip proxy server port 10.44.2.3. Cek dengan perintah env | grep -i proxy.

1.  Client hanya dapat mengakses internet diluar (selain) hari & jam kerja (senin-jumat 08.00 - 17.00) dan hari libur (dapat mengakses 24 jam penuh)

2.  Adapun pada hari dan jam kerja sesuai nomor (1), client hanya dapat mengakses domain loid-work.com dan franky-work.com (IP tujuan domain dibebaskan)

3.  Saat akses internet dibuka, client dilarang untuk mengakses web tanpa HTTPS. (Contoh web HTTP: <http://example.com>)

4.  Agar menghemat penggunaan, akses internet dibatasi dengan kecepatan maksimum 128 Kbps pada setiap host (Kbps = kilobit per second; lakukan pengecekan pada tiap host, ketika 2 host akses internet pada saat bersamaan, keduanya mendapatkan speed maksimal yaitu 128 Kbps)

5.  Setelah diterapkan, ternyata peraturan nomor (4) mengganggu produktifitas saat hari kerja, dengan demikian pembatasan kecepatan hanya diberlakukan untuk pengaksesan internet pada hari libur\
Setelah proxy Berlint diatur oleh Loid, dia melakukan pengujian dan mendapatkan hasil sesuai tabel berikut.

|

Aksi

 |

Senin (10.00)

 |

Senin (20.00)

 |

Sabtu (10.00)

 |
|

Akses internet (HTTP)

 |

x

 |

x

 |

x

 |
|

Akses internet (HTTPS)

 |

x

 |

v

 |

v

 |
|

Akses loid-work.com dan franky-work.com

 |

v

 |

x

 |

x

 |
|

Speed limit (128Kbps)

 |

tidak bisa akses

 |

x (speed tidak dibatasi)

 |

v 

 |

x: tidak

v: iya

Sesuai dengan perintah diatas, terdapat 5 ketentuan yang harus dipenuhi

Untuk ketentuan keempat(4), diberikan ketentuan berupa pembatasan internet sebesar 128kbps. Disini kita akan melakukan sesuai dengan modul dimana untuk membatasi bandwith kita harus membuat file dengan command nano /etc/squid/acl-bandwidth.conf.

Kemudian, kita masukkan script :

delay_pools 1

delay_class 1 1

delay_access 1 allow all

delay_parameters 1 16000/64000

Jika sudah, ubah konfigurasi file squid.conf menjadi :

include /etc/squid/acl-bandwidth.conf

http_port 8080

visible_hostname Berlint

http_access allow all

Jika sudah restart squid, dan lakukan speed tes. Berikut adalah speedtest sebelum dan sesudah dibatasi bandwithnya.

![](https://lh6.googleusercontent.com/HzmeZrpVdwAczfb_ark9xfjlXwiINrU3mWdVl7bY7pzvOawoCD879Yf2_RBED-_z_m1DsEUgbAkKXlc32OWurp6-O_501vsdCJl_qy-eQvhjr22X3ttmTjl1I7ZF1B_nJWoTEh2kGs5uWYDi7qssLLtGGkR_eb7wxJOXIreSfV7II2U2u521nvKPgXTlGQ)

![](https://lh6.googleusercontent.com/dlxKiJEAfdEPwjrb2fKd3bZFIlvDb4Tr_yIhx7011lsEvulJGHUVQ5_JgsyImuwzgLxJg-9jBQlYpYVL1Mf6Wcads-67YBcnnw4NKcMJeR_7I3hPtiXIed2-e4AsbdxK8waHDL3G7eqfK3s3T7YlSUVzSFdL8RtQDl689XoD9LksA7Vw9cu-Nsc1DMX6kw)

Untuk ketentuan ketiga(3), client perlu dilarang untuk mengakses web yang hanya http atau hanya menggunakan https. Disini sesuai dengan modul, kita membuat agar hanya website dengan https yang bisa diakses dengan mengubah file nano /etc/squid/squid.conf. Disini kita bisa melihat bahwa http_access allow all diubah menjadi http_access deny all. 

![](https://lh5.googleusercontent.com/Br_RdgTH9AxSF4wUBeA_eMJEVlEVhmVCO2Ev0WC8PVilLK4jUEix7nHrBlTx-iP1FGzG5t5wc5gmmlxPmA94g1Zo3GBpPlBtXYcatQzAFB0gQmn6vfQ8A89rTkw5nsebvYjiJASEiXrZIue87utzpT5nX2tm4lh-wpY0j4g0KeL15dHjf75CNDTit7C_wg)

Jika sudah, restart squid berlint, dan lakukan lynx google.com di salah satu client dari proxy server. Jika berhasil, maka seharusnya client tidak dapat mengakses website tersebut.

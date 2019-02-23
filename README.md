# xtra-daemon
Research on xtra-daemon, a Qualcomm Technologies, Inc. proprietary driver<br>
on Qualcomm equiped devices. e.g. Android Smartphones

# Why?
When observing Network traffic on Android Smartphones with whireshark,<br> 
connections to Qualcomm Servers are started regulary.

# Research
Reason is a proprietary Qualcomm driver named xtra-daemon. <br>
Connections are started to izatcloud.net domain.

# Description by Qualcomm
Archive: https://github.com/fogfon/xtra-daemon/blob/master/Description%20by%20Qualcomm <br>
WWW: https://www.qualcomm.com/site/privacy/services at 2019/02/23

# Thoughts
Yes, it is a service for better user experience, faster location calculation, less battery consumption... <br>
Away from the planned or intended course it is a service that tracks every qualcomm equiped cellphone worlwide

# Tests
We tested Android 7.1 and Android 8.1 firmware of several devices running LineageOS 14.1 or 15.1.<br>
We saw some differences:<br>
On Android 7.1 firmware: Connections to izatcloud.net domain is starting unencrypted!!! after boot completed.<br>
On Android 8.1 firmware: Connections to izatcloud.net domain is starting encrypted when using gps.<br>

# Examples
BQ X2 LOS_15.1<br>
419	431.779843598	10.42.0.1	10.42.0.182	DNS	252	Standard query response 0x9645 A xtrapath3.izatcloud.net CNAME xtrapath3.qcomgeo2.com CNAME xp3.gpsonextra.net CNAME d3nj9ptoklgw8o.cloudfront.net A 52.222.231.102 A 52.222.231.26 A 52.222.231.218 A 52.222.231.191<br>
420	431.786273878	10.42.0.182	52.222.231.102	TCP	74	40509 → 443 [SYN] Seq=0 Win=65535 Len=0 MSS=1460 SACK_PERM=1 TSval=1585 TSecr=0 WS=256<br>
421	431.824837142	52.222.231.102	10.42.0.182	TCP	74	443 → 40509 [SYN, ACK] Seq=0 Ack=1 Win=28960 Len=0 MSS=1460 SACK_PERM=1 TSval=1329662173 TSecr=1585 WS=256<br>
422	431.829302923	10.42.0.182	52.222.231.102	TCP	66	40509 → 443 [ACK] Seq=1 Ack=1 Win=87808 Len=0 TSval=1590 TSecr=1329662173<br>

BQ U LOS_14.1 Unencrypted!!!!!<br>
24	84.846798397	10.42.0.1	10.42.0.143	DNS	252	Standard query response 0xe495 A xtrapath3.izatcloud.net CNAME xtrapath3.qcomgeo2.com CNAME xp3.gpsonextra.net CNAME d3nj9ptoklgw8o.cloudfront.net A 54.240.186.152 A 54.240.186.95 A 54.240.186.227 A 54.240.186.89<br>
27	84.930149134	10.42.0.143	54.240.186.152	TCP	74	58343 → 80 [SYN] Seq=0 Win=65535 Len=0 MSS=1460 SACK_PERM=1 TSval=109 TSecr=0 WS=256<br>
39	85.049953417	54.240.186.152	10.42.0.143	TCP	66	80 → 58343 [ACK] Seq=1 Ack=514 Win=30208 Len=0 TSval=1378647981 TSecr=115
..... ongoing unencrypted<br>
66	85.202479389	54.240.186.152	10.42.0.143	TCP	1294	80 → 58343 [ACK] Seq=30701 Ack=514 Win=30208 Len=1228 TSval=1378647997 TSecr=115 [TCP segment of a reassembled PDU]<br>
68	85.232714518	10.42.0.143	54.240.186.152	TCP	66	58343 → 80 [ACK] Seq=514 Ack=1229 Win=90112 Len=0 TSval=139 TSecr=1378647982<br>

BQ X LOS_15.1 Unencrypted!!!!!<br>
40	6.444926775	10.42.0.1	10.42.0.184	DNS	252	Standard query response 0xd0ae A xtrapath2.izatcloud.net CNAME xtrapath2.qcomgeo2.com CNAME xp2.gpsonextra.net CNAME d3bfhz8j7i21uk.cloudfront.net A 13.35.253.70 A 13.35.253.29 A 13.35.253.98 A 13.35.253.22<br>
41	6.450952349	10.42.0.184	13.35.253.70	TCP	74	59039 → 80 [SYN] Seq=0 Win=65535 Len=0 MSS=1460 SACK_PERM=1 TSval=4294961497 TSecr=0 WS=256<br>
48	6.474747967	13.35.253.70	10.42.0.184	TCP	74	80 → 59039 [SYN, ACK] Seq=0 Ack=1 Win=28960 Len=0 MSS=1460 SACK_PERM=1 TSval=905841779 TSecr=4294961497 WS=256<br>
51	6.478261819	10.42.0.184	13.35.253.70	TCP	66	59039 → 80 [ACK] Seq=1 Ack=1 Win=87808 Len=0 TSval=4294961499 TSecr=905841779<br>
58	6.809370294	13.35.253.70	10.42.0.184	TCP	66	80 → 59039 [ACK] Seq=1 Ack=521 Win=30208 Len=0 TSval=905841813 TSecr=4294961530<br>

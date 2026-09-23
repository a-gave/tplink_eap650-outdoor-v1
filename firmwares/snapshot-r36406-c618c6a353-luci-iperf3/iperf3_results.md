from localhost
```
root@OpenWrt:~# iperf3 -c 127.0.0.1
Connecting to host 127.0.0.1, port 5201
Accepted connection from 127.0.0.1, port 34916
[  5] local 127.0.0.1 port 34928 connected to 127.0.0.1 port 5201
[  5] local 127.0.0.1 port 5201 connected to 127.0.0.1 port 34928
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-1.00   sec   161 MBytes  1.35 Gbits/sec                  
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.01   sec   163 MBytes  1.36 Gbits/sec    0   1.19 MBytes       
[  5]   1.00-2.00   sec   168 MBytes  1.41 Gbits/sec                  
[  5]   1.01-2.00   sec   166 MBytes  1.40 Gbits/sec    0   1.19 MBytes       
[  5]   2.00-3.00   sec   168 MBytes  1.41 Gbits/sec                  
[  5]   2.00-3.00   sec   168 MBytes  1.41 Gbits/sec    0   1.19 MBytes       
[  5]   3.00-4.00   sec   173 MBytes  1.45 Gbits/sec                  
[  5]   3.00-4.00   sec   164 MBytes  1.37 Gbits/sec    0   1.19 MBytes       
[  5]   4.00-5.00   sec   159 MBytes  1.34 Gbits/sec    0   1.19 MBytes       
[  5]   4.00-5.00   sec   176 MBytes  1.47 Gbits/sec                  
[  5]   5.00-6.00   sec   179 MBytes  1.50 Gbits/sec    0   1.19 MBytes       
[  5]   5.00-6.00   sec   180 MBytes  1.51 Gbits/sec                  
[  5]   6.00-7.00   sec   182 MBytes  1.53 Gbits/sec                  
[  5]   6.00-7.00   sec   182 MBytes  1.53 Gbits/sec    0   1.19 MBytes       
[  5]   7.00-8.00   sec   187 MBytes  1.57 Gbits/sec                  
[  5]   7.00-8.00   sec   180 MBytes  1.51 Gbits/sec    0   1.19 MBytes       
[  5]   8.00-9.00   sec   188 MBytes  1.58 Gbits/sec                  
[  5]   8.00-9.00   sec   103 MBytes   863 Mbits/sec    0   1.19 MBytes       
[  5]   9.00-10.00  sec   189 MBytes  1.58 Gbits/sec                  
[  5]  10.00-10.00  sec   128 KBytes  1.03 Gbits/sec                  
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-10.00  sec  1.73 GBytes  1.49 Gbits/sec                  receiver
[  5]   9.00-10.00  sec   111 MBytes   929 Mbits/sec    0   1.19 MBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  1.73 GBytes  1.49 Gbits/sec    0            sender
[  5]   0.00-10.00  sec  1.73 GBytes  1.49 Gbits/sec                  receiver

iperf Done.
```


from a client connected to the lan port
```
<redacted>:~$ iperf3 -c 192.168.1.1 --bidir
Connecting to host 192.168.1.1, port 5201
[  5] local 192.168.1.19 port 54890 connected to 192.168.1.1 port 5201
[  7] local 192.168.1.19 port 54902 connected to 192.168.1.1 port 5201
[ ID][Role] Interval           Transfer     Bitrate         Retr  Cwnd
[  5][TX-C]   0.00-1.00   sec  66.9 MBytes   560 Mbits/sec   29    643 KBytes       
[  7][RX-C]   0.00-1.00   sec  56.0 MBytes   469 Mbits/sec                  
[  5][TX-C]   1.00-2.00   sec  64.8 MBytes   543 Mbits/sec    0    710 KBytes       
[  7][RX-C]   1.00-2.00   sec  59.2 MBytes   497 Mbits/sec                  
[  5][TX-C]   2.00-3.00   sec  45.6 MBytes   383 Mbits/sec   10    543 KBytes       
[  7][RX-C]   2.00-3.00   sec  78.6 MBytes   660 Mbits/sec                  
[  5][TX-C]   3.00-4.00   sec  62.2 MBytes   522 Mbits/sec    0    624 KBytes       
[  7][RX-C]   3.00-4.00   sec  63.6 MBytes   534 Mbits/sec                  
[  5][TX-C]   4.00-5.00   sec  62.2 MBytes   522 Mbits/sec    0    694 KBytes       
[  7][RX-C]   4.00-5.00   sec  64.4 MBytes   540 Mbits/sec                  
[  5][TX-C]   5.00-6.00   sec  49.0 MBytes   411 Mbits/sec    1    527 KBytes       
[  7][RX-C]   5.00-6.00   sec  78.2 MBytes   656 Mbits/sec                  
[  5][TX-C]   6.00-7.00   sec  30.2 MBytes   254 Mbits/sec    0    564 KBytes       
[  7][RX-C]   6.00-7.00   sec  95.8 MBytes   803 Mbits/sec                  
[  5][TX-C]   7.00-8.00   sec  47.2 MBytes   396 Mbits/sec    0    617 KBytes       
[  7][RX-C]   7.00-8.00   sec  80.5 MBytes   675 Mbits/sec                  
[  5][TX-C]   8.00-9.00   sec  56.0 MBytes   470 Mbits/sec    0    680 KBytes       
[  7][RX-C]   8.00-9.00   sec  70.9 MBytes   595 Mbits/sec                  
[  5][TX-C]   9.00-10.00  sec  56.0 MBytes   470 Mbits/sec   13    518 KBytes       
[  7][RX-C]   9.00-10.00  sec  70.9 MBytes   594 Mbits/sec                  
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID][Role] Interval           Transfer     Bitrate         Retr
[  5][TX-C]   0.00-10.00  sec   540 MBytes   453 Mbits/sec   53            sender
[  5][TX-C]   0.00-10.01  sec   538 MBytes   450 Mbits/sec                  receiver
[  7][RX-C]   0.00-10.00  sec   721 MBytes   605 Mbits/sec    0            sender
[  7][RX-C]   0.00-10.01  sec   718 MBytes   602 Mbits/sec                  receiver

iperf Done.
```


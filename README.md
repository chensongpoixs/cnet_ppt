# cnet_ppt
谢希仁老师的计算机网络PPT讲义






使用Curl命令查看请求响应时间方法

curl命令查看请求响应时间的方法非常简单，今天小编抽空给大家介绍下使用Curl命令查看请求响应时间方法，感兴趣的朋友一起看看吧

curl命令查看请求响应时间

# curl -o /dev/null -s -w %{time_namelookup}::%{time_connect}::%{time_starttransfer}::%{time_total}::%{speed_download}"\n" 
http://www.36nu.com 
0.014::0.015::0.018::0.019::1516256.00
-o：把curl 返回的html、js 写到垃圾回收站[ /dev/null]

-s：去掉所有状态

-w：按照后面的格式写出rt

time_namelookup：DNS 解析域名www.36nu.com的时间

time_commect：client和server端建立TCP 连接的时间

time_starttransfer：从client发出请求；到web的server 响应第一个字节的时间

time_total：client发出请求；到web的server发送会所有的相应数据的时间

speed_download：下周速度 单位 byte/s

上面这条命令及返回结果可以这么理解：

0.014: DNS 服务器解析www.36nu.com 的时间单位是s

0.015: client发出请求，到c/s 建立TCP 的时间；里面包括DNS解析的时间

0.018: client发出请求；到s响应发出第一个字节开始的时间；包括前面的2个时间

0.019: client发出请求；到s把响应的数据全部发送给client；并关闭connect的时间

1516256.00 ：下载数据的速度

建立TCP连接到server返回client第一个字节的时间：0.018s – 0.015s = 0.003s

server把响应数据发送给client的时间：0.019s – 0.018 = 0.01s




测试案例:


post 请求:


>curl -o /dev/null -s -w %{time_namelookup}::%{time_connect}::%{time_starttransfer}::%{time_total}::%{speed_download}"\n"  192.168.1.15/admin/game/list_game.php -X POST -H "Content-Type:application/json" -d '{"player_id":32429, "start_timestamp":0, "end_timestamp":9000000000}'  

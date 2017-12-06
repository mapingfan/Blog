# Redis初探

标签（空格分隔）： Redis

---

今天第一次接触`Redis`，感觉十分新奇。虽然本科时候已经接触过`NoSQL`，但是对于这种`KV`键值数据库，还是第一次接触。
今天使用`IDEA`写`Demo`时，发现竟然连接不上服务器上的`Redis`数据库。修了半小时，问题还是解决不了，后来就直接拿着错误信息错`Google`。最终在`StackOverflow`上找到了答案，下面简单记录下。
首先看下错误信息
```
redis.clients.jedis.exceptions.JedisConnectionException: java.net.ConnectException: Connection refused
    at redis.clients.jedis.Connection.connect(Connection.java:164)
    at redis.clients.jedis.BinaryClient.connect(BinaryClient.java:80)
    at redis.clients.jedis.Connection.sendCommand(Connection.java:100)
    at redis.clients.jedis.Connection.sendCommand(Connection.java:95)
    at redis.clients.jedis.BinaryClient.ping(BinaryClient.java:93)
    at redis.clients.jedis.BinaryJedis.ping(BinaryJedis.java:105)
    at TestRedis.main(TestRedis.java:14)
Caused by: java.net.ConnectException: Connection refused
    at java.net.PlainSocketImpl.socketConnect(Native Method)
    at java.net.AbstractPlainSocketImpl.doConnect(AbstractPlainSocketImpl.java:339)
    at java.net.AbstractPlainSocketImpl.connectToAddress(AbstractPlainSocketImpl.java:200)
    at java.net.AbstractPlainSocketImpl.connect(AbstractPlainSocketImpl.java:182)
    at java.net.SocksSocketImpl.connect(SocksSocketImpl.java:392)
    at java.net.Socket.connect(Socket.java:579)
    at redis.clients.jedis.Connection.connect(Connection.java:158)
    ... 6 more
```
从上面可以看到，连接被拒绝了。起初我想可能防火墙端口没开，跑到服务器上把`6379`端口开启，然后还是连不上。在`Linux`上开启防火墙，可以使用`ufw`命令，如果没有，需要先安装`sudo apt-get install ufw`。
然后输入相关命令就可以开启端口。
在解决端口问题后，还是连不上，下面提供一种新的解决方案：
```

There are a few settings that would affect this: bind and protected-mode. They work together to provide a baseline of security with new installs.

Find the following in your redis.conf file and comment it out:

bind 127.0.0.1

By adding a # in front of it:

# bind 127.0.0.1

Or, if you would rather not comment it out, you can also add the IP if your eth0/em1 interface to it, like this:

bind 127.0.0.1 192.168.1.57

Also, unless you're using password security, you'll also have to turn off protected mode by changing:

protected-mode yes

To:

protected-mode no

Make sure that you read the relevant documentation and understand the security implications of both of these changes.

After making these changes, restart redis.

```
[原文链接][1]在这里。在这里要注意`protected-mode no`这个配置。


  [1]: https://stackoverflow.com/questions/37867633/cannot-connect-to-redis-using-jedis/37868169#37868169
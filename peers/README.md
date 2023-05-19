### 对等点列表

我们向 tracker 发送一个 get 请求，携带 `info_hash` 和 `peer_id` 的query参数.得到一个编码响应
```
d
  8:interval
    i900e
  5:peers
    252:(another long binary blob)
e
```
Interval告诉我们应该多久再次连接到跟踪器以刷新我们的对等点列表。值 900 意味着我们应该每 15 分钟（900 秒）重新连接一次。

Peers是另一个包含每个对等方 IP 地址的长二进制 blob。它由六个字节组成。每组中的前四个字节代表对等方的 IP 地址——每个字节代表 IP 中的一个数字。最后两个字节代表端口，作为 big-endian uint16。Big-endian或network order意味着我们可以通过将一组字节从左到右挤压在一起来将它们解释为整数。

![](https://blog.jse.li/torrent/address.png)
### 完成握手

#### 建立tcp连接
```go
conn, err := net.DialTimeout("tcp", peer.String(), 3*time.Second)
if err != nil {
    return nil, err
}
```

#### 握手
![](https://blog.jse.li/torrent/handshake.png)

BitTorrent 握手的报文由五个部分组成：

- 协议标识符的长度，始终为 19（十六进制为 0x13）
- 协议标识符，称为**pstr**，它总是 `BitTorrent protocol`
- 八个保留字节，全部设置为 0。我们将其中一些翻转为 1 以指示我们支持某些扩展。但我们不这样做，所以我们将它们保持为 0
- 我们之前计算的infohash来识别我们想要的文件
- 我们为识别自己而制作的Peer ID

放在一起，握手字符串可能如下所示：
```
\x13BitTorrent protocol\x00\x00\x00\x00\x00\x00\x00\x00\x86\xd4\xc8\x00\x24\xa4\x69\xbe\x4c\x50\xbc\x5a\x10\x2c\xf7\x17\x80\x31\x00\x74-TR2940-k8hj0wgej6ch
```
mesh IV Index



1. 用途
2. IV Index 更新过程
3. IVI 的作用？
4. IV Update procedure 里各个时间段的作用？



IV Update 过程最小 8 天时间，因此节点发送数据频率不能超过 24 Hz，否则 Sequence Number（24-bit）会不够用。
$$
2^{24} \div (8 \times 24 \times 60 \times 60) \approx 24\ Hz
$$


## IV Update procedure

state of operation:

- Normal Operation
- IV Update in Progress





## IVI 的作用

已知节点当前的 IV Index 为 **N**，接收的 Network PDU 里 IVI 的值为 **ivi**，若：

- ivi == N & 0x01 : 使用值为 **N** 的 IV Index 接收网络包。
- ivi !=  N & 0x01 : 使用值为 **N-1** 的 IV Index 接收网络包。

怎么理解这个操作呢？IVI 的来源就是 IV Index 的最低有效位，

- 若发送方和接收方的 IV Index 一致，那么这两个 IV Index 计算出的 IVI 也是一致，因此就使用当前的 IV Index 接收即可。
- 若发送方和接收方的 IV Index 不一致，那么这两个 IV Index 计算出的 IVI 也不一致，尝试使用当前的 IV Index - 1 接收。
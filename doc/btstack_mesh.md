

Link ID 在整个会话（session）期间保持不变，利用随机数生成。

利用 Device UUID 标识 Unprovisioned device 。

Generic Provisioning PDU 需要延时 20 ~ 50 ms 的随机时间发送。

每一个 bearer 都有一个 MTU，当 Provisioning PDU 需要分段时，每一段都需要填满这个 bearer 的 MTU，最后一个段除外。

30 s 内未收到 Transaction Acknowledgment 消息，取消本次 transaction，取消 provisioning 流程，关闭 Link 。







Proxy Protocol  分段重组

首先确定发送 PDU 的最大大小 `MESH_PROV_MAX_PROXY_PDU`，并利用此大小创建一个数组用于存储数据。用一个 `offset` 变量记录数组里的当前索引，每次有数据到来，就根据 `offset` 将数据存入相应位置处即可。**注意不要造成数组越界。**


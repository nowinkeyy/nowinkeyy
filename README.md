### Hi there 👋

<!--
**nowinkeyy/nowinkeyy** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->

- 🔭 I’m currently working on labring/sealos...

[![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=nowinkeyy&count_private=true&show_icons=true&hide=stars)](https://github.com/anuraghazra/github-readme-stats)


### My Contributions 👋

Apache RocketMQ

提案: [RIP-52] Optimize Building ConsumeQueue（优化构建消费队列）[提案链接](https://github.com/apache/rocketmq/wiki/RIP-52-Optimize-Building-ConsumeQueue)

背景介绍：消息的生产和消息的消费与 CommitLog 和 ConsumeQueue 两个日志文件有关，Producer 发送消息给 Broker，Broker 将消息写入 CommitLog，然后根据 CommitLog 异步生成 ConsumeQueue，最后 Consumer 消费 ConsumeQueue 中的消息。

问题：随着集群规模增大，消息生产流量增大。单线程构建 ConsumeQueue 的速度跟不上消息写入 CommitLog 的速度，导致出现消费延迟问题。

解决方案：构建 ConsumeQueue 的过程主要分为校验过程和写入过程，将 CommitLog 消息切片并编号，使用多个线程来并发校验 CommitLog 消息切片，将校验好的 CommitLog 消息切片排好序，然后使用单个线程按顺序将 CommitLog 消息切片写入 ConsumeQueue。

亮点：
- 代码遵从开闭原则，使用 Reactor 模式
- 充分利用磁盘缓存机制，避免磁盘冷读
- 极大提高了构建消费队列的速度，解决了消费延迟的问题

# 核验记录

核验日期：2026-10-02（北京时间）。

- [Reth minimal](https://reth.rs/run/storage/minimal/)：本次页面标示v2.7.0；Storage V2在区块24,396,823测得224GB。minimal保留近期收据和有限历史状态，不能承担完整历史查询。该测量不是当前机器总容量或同步峰值保证；本次未验证作者所述2.5+版本及所有模拟接口。
- [以太坊区块文档](https://ethereum.org/developers/docs/blocks)：12秒slot可能漏块，不能当成12秒必出块的保证。未核实未来6秒slot的生效安排。
- [Flashbots入块排查](https://docs.flashbots.net/flashbots-auction/advanced/troubleshooting)：交易包模拟失败、激励不足、竞价冲突、迟到都可能阻止入块；Gas效率和递交速度仍有意义。并非所有Builder都遵循同一种简化排序规则。
- [TypeScript类型文档](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)：any会关闭相关类型检查；语言静态类型不能替代运行时输入验证与数值语义检查。

未独立核验：服务器型号与现价、2026年涨价记录、作者收益、市占率截图采样方法、Geth接口合入历史、完整RPC兼容性。图中投票样本分别为13与29人。小报童前文未读取；评论未获取。

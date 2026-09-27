# 先配置 CYBER_API_KEY、CYBER_MODEL、CYBER_BASE_URL、TYPESAFE_API_KEY。
# JEV_BENCH_PRICES 是包含上述两个模型实际价格的 JSON；可选 CYBER_PROVIDER。
$env:JEV_BENCH_LIVE = '1'
$env:JEV_BENCH_REPORT = 'D:\path\to\jev-live.json'
go test -tags full ./pkg/exts/jev -run '^TestLiveAutomaticReflexABC$' -count=1 -v -timeout 120m
```

每个场景从空库运行同样的三组普通任务，默认每组 40 个训练任务，至少 20 个配对留出任务，轮换 A/B/C 顺序。没有预置规则、手动激活或任务中的 Reflex 提示。场景是浏览器多步向导（重排、延迟、重绘、新文本）和四端点 HTTP 独立证据检查（包含失败证据）。结果由浏览器最终状态、服务端动作/请求记录及最终答案共同检查。

报告在每个完成的任务后写入，保留前台与包含学习的耗时、前台 L2 次数、全部 L2/JEV 请求和用量、cache/reasoning、费用是否完整、正确性与模型调用记录。`JEV_BENCH_PRICE_SOURCE` 标记价格来源；使用参考价格时，费用结果只是估算，不代表代理供应商实际账单。编译/标签映射/重放/失败请求计入费用；reasoning 是 output 的子集，不重复计费。冷启动额外费用与达到收支平衡的任务数单独报告。

浏览器目标：留出任务 L2 次数减少 ≥50%，全部 L2 output 减少 ≥30%，reasoning 已报告时同样减少 ≥30%，中位耗时减少 ≥20%，p95 退化 ≤10%。aiscan 目标：中位耗时和费用各减少 ≥15%，p95 退化 ≤10%。任何正确性失败、未知费用或无法自动激活均不能通过。

真实模型验收需要有效凭据和真实价格。没有这些条件时测试明确 SKIP，机制测试的数字不应当写成生产性能结论。


 # GPU 选择 
## 先上结论
- 10万元以下 ，2张RTX A6000 48GB，性价比最高；  
- 15万元， 系统整体性价比最高4张RTX A6000 48GB；  
- 30万元 ，2张A100 80GB  
  
  
  
根据最近我的使用结果，基于已有LLM全参数微调  
  
用DeepSpeed offload到CPU上，可以极大节省显存，甚至极端情况下24GB就够了  

> "zero_optimization": {  
"stage": 3,  
"offload_optimizer": {  
"device": "cpu",  
"nvme_path": null  
},  
"offload_param": {  
"device": "cpu",  
"nvme_path": null  
},  
"stage3_gather_16bit_weights_on_model_save": trueBlockquote
  
RTX6000 ADA GPU使用率在 50%左右，PCI-E 4.0 带宽使用率约 21%，这个时候瓶颈基本在 CPU 单核性能上。  
![enter image description here](%28https://static.chiphell.com/forum/202307/10/094140c80g7febgzebbfg5.jpg)
需要注意的是前期数据准备阶段 PCI-E 4.0 带宽使用率约 80~85%，GPU 使用率约 99%,大约持续 11 小时。  
  
2.5 万条数据，每步大约需要 25~ 30 秒（bs=1），估算每跑一遍数据大约需要大约 8.7 天；如果将 bs=7，每步大约需要 45~51 秒 60 秒，估算每跑一遍数据大约需要大约 2.1 天 2.5 天  
![enter image description here](https://static.chiphell.com/forum/202307/10/094318hk2kfkpofugkfk2w.png)

因为 DeepSpeed offload 到 CPU 后，瓶颈是 CPU（目前暂不支持多线程），因此现阶段影响 LLM 全参数微调时间的因素就是显存，很明显这时高显存能带来极大的性能收益。  
目前电脑支持4张显卡的计算是装机的一个瓶颈，瓶颈包含 10A 插座、制冷、机箱大小、稳定和物理安全等  
DeepSpeed offload 到 CPU 后：  
假设每个样本需要 5 GB  

## 系统成本约 5 万~10 万：  
4 张 RTX 3090 或 4 张 RTX4090，计算性能上整体一致（RTX4090 有一定优势，但成本明显偏高），4 卡大约96GB 显存，实际可用（假设 6B 模型），大约（24GB-6GB-6GB） $*$ 4=12 GB $*$ 4 bs 约等于 8    
2 张 RTX A6000，2 张卡大约 96 GB显存，实际可用（假设 6B 模型），大约（48GB-6GB-6GB）*2=32 GB*2 bs约等于 12  
目前 RTX A6000 在 2.75 万；RTX 3090 在0 .85 万元（怕着火只能用新的）；RTX 4090 在 1.5 万元；  
系统基本成本约 2.5 万，RTX A6000 $*$ 2 =5.5 万；RTX 3090 $*$ 4=3.4 万元（4 卡散热、电源、组装、维护成本上升）；RTX 4090 $*$ 4=6 万元（4 卡散热、电源、组装、维护成本上升）  
在这里推荐 2 张 RTX A6000  
    
## 系统成本约15万：  
4 张 RTX A6000 或 2 张 RTX 6000 ADA，价格上整体一致，  
4 张 RTX A6000 大约 192GB 显存，实际可用（假设6B模型），大约（48GB-6GB-6GB） $*$ 4=36GB*4 bs约等于24  
2 张 RTX 6000 ADA 大约 96GB 显存，实际可用（假设6B模型），大约（48GB-6GB-6GB） $*$ 2=72GB bs约等于12  
1 张 A100 80GB，实际可用（假设 6B 模型），大约（80GB-6GB-6GB） $*$ 1=68GB bs 约等于 13 
目前 RTX A6000 在 2.75 万；RTX 6000 ADA 在 5.1 万元；  
在这里推荐 4 张 RTX A6000  
## 系统成本约 30 万：  
这个该考虑 A100 80GB 啦，优势太大了；  
1 张 A100 80 GB，实际可用（假设 6B 模型），大约（80GB-6GB-6GB）$*$ 1=68GB bs约等于13  
2 张 A100 80 GB，实际可用（假设 6B 模型），大约（80GB-6GB-6GB）$*$ 2=68GB*2 bs约等于26  
实际上 2 张 A100 80GB 已经超神了，性能可能更强，因为支持 nvlink  
在这里推荐 2 张 A100 80GB

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMDcwMzkyODldfQ==
-->
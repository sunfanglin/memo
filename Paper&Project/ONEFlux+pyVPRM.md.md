# 基于标准化后藏北高原 CO2 通量数据的标准化的 vprm 参数确定
## 青藏高原通量网：
- 收集高原上涡动观测数据，使用 ONEFlux 进行标准化评估，建立数据集；
-- 质量控制；
-- 数据插补；
-- 质量评估。
- 结合卫星数据，使用 pyVPRM 测算所有站点 vprm 计算参数。

结合 ONEFlux 和 pyVPRM
实地调查，仪器安装状态，地表情况

一方面数据堆积如山，另一方面，应用者无数据可用。
原因是，数据碎片化，数据观测者没有精力完成数据质量和调用性的标准化。应用者没有精力从头筛选海量数据。

如 一些模型已经做好了标准化的数据调用接口，但是没有足够的标准化数据来使用。

pyVRPM 就是使用 oneflux 的输出来确定植被呼吸光合过程的计算参数。

传统的确定过程繁琐，可重复性差。

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUzNTU2Nzk3OCwtNTMyMzc1MzU2LDE5NT
gzMzU4OTgsMTY5Nzc0NzAyNSwtNzQzNTI0MTA2XX0=
-->
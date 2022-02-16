# Windows-Time-of-Day-QoS

Windows上基于策略的QoS本身没有计划任务的功能  
摸索了一下，本地组策略中的任何修改，当然也包括基于策略的QoS的配置会保存成一个文件("C:\Windows\System32\GroupPolicy\Machine\Registry.pol"
)，通过强制刷新组策略来启用(写到注册表中?)
由于发现了QoS的配置其实是文件,因此可以通过替换两个版本的文件来实现根据时间控制QoS

整体的流程大体是：
修改QoS(忙时QoS)->强制刷新组策略->复制第一份Registry.pol副本
修改QoS(闲时QoS)->强制刷新组策略->复制第二份Registry.pol副本
根据需求制作 任务计划程序(复制副本至原目录C:\Windows\System32\GroupPolicy\Machine\->强制刷新组策略）

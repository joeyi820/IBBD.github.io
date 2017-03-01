# 产品迭代及发布流程规范
对于大型项目，因为涉及的人员比较多，而产品迭代周期又比较快，这时需要相应的流程，来规范发布流程，尽量做到平滑升级，保障产品稳定。从环节上主要分成以下的步骤：

- 本地开发环境：大家在本地开发时使用的环境
- 开发环境：这是一个共同的给开发工程师使用的环境，使用master分支，多人同时开发时需要。
- 测试环境：这个环境主要个测试工程师使用，当产品的里程碑开发完成之后，代码合并到release分支并在测试服务器更新。
- 预发布环境：该环境就是正式环境的一部分，但是只是将负载均衡中的某些流量，正式的用户并不能访问该系统（例如对于一个网站系统，预发布时系统连接都是正式的数据库等，但是该系统还不能给网站的正式用户访问到）。在增加新模块或者新功能时，可能需要使用该环境。
- 灰度环境：这是完全正式的环境，正式用户也是能访问的，只是其所占的流量比较少，有问题可以将影响减到最小。
- 正式环境：这就是生产环境了。

在实践中，并不是每次发布都是需要进入预发布环境，对于小版本的迭代可能直接进入灰度环境。

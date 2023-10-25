# AutoDock Vina Ehpc计算巢快速部署

>**免责声明：**本服务由第三方提供，我们尽力确保其安全性、准确性和可靠性，但无法保证其完全免于故障、中断、错误或攻击。因此，本公司在此声明：对于本服务的内容、准确性、完整性、可靠性、适用性以及及时性不作任何陈述、保证或承诺，不对您使用本服务所产生的任何直接或间接的损失或损害承担任何责任；对于您通过本服务访问的第三方网站、应用程序、产品和服务，不对其内容、准确性、完整性、可靠性、适用性以及及时性承担任何责任，您应自行承担使用后果产生的风险和责任；对于因您使用本服务而产生的任何损失、损害，包括但不限于直接损失、间接损失、利润损失、商誉损失、数据损失或其他经济损失，不承担任何责任，即使本公司事先已被告知可能存在此类损失或损害的可能性；我们保留不时修改本声明的权利，因此请您在使用本服务前定期检查本声明。如果您对本声明或本服务存在任何问题或疑问，请联系我们。

## 概述

分子对接（Molecular docking）是虚拟药物筛选中的关键环节。AutoDock Vina作为一款开源的分子对接软件，具有速度快、算法准确等优点，特别适用于搭建基于分子对接的虚拟筛选，它基于MGLTools工具包进行使用。MGLTools包括AutoDock Tools（ADT）和Python Molecular Viewer（PMV）。ADT用来为Vina生成输入文件，PMV用来查看结果。更多信息，请参见AutoDock Vina和MGLTools。

## 前提条件

部署AutoDock Vina社区版服务实例，需要对部分阿里云资源进行访问和创建操作。因此您的账号需要包含如下资源的权限。
  **说明**：当您的账号是RAM账号时，才需要添加此权限。

| 权限策略名称                          | 备注                     |
|---------------------------------|------------------------|
| AliyunECSFullAccess             | 管理云服务器服务（ECS）的权限       |
| AliyunVPCFullAccess             | 管理专有网络（VPC）的权限         |
| AliyunROSFullAccess             | 管理资源编排服务（ROS）的权限       |
| AliyunEHPCFullAccess             | 管理弹性高性能计算（EHPC）的权限       |
| AliyunNASFullAccess             | 管理文件存储（NAS）的权限       |
| AliyunComputeNestUserFullAccess | 管理计算巢服务（ComputeNest）的用户侧权限 |


## 计费说明

AutoDock Vina社区版在计算巢部署的费用主要涉及：

- 弹性高性能计算集群（EHPC）费用
- 文件系统（NAS）费用
- 流量带宽费用

## 部署架构
<img src="1.png" width="1500" height="700" align="bottom"/>

- 部署由一个ehpc集群组成，ehpc集群中包括manager节点、schedule节点和compute节点
- 服务使用nas-cpfs构建高性能共享文件系统

## 参数说明
| 参数组       | 参数项      | 说明                                                                     |
|-----------|----------|------------------------------------------------------------------------|
| 服务实例      | 服务实例名称   | 长度不超过64个字符，必须以英文字母开头，可包含数字、英文字母、短划线（-）和下划线（_）                          |
|           | 地域       | 服务实例部署的地域                                                              |
|           | 付费类型     | 资源的计费类型：按量付费和包年包月                                                      |
| EHPC集群配置  | 集群登录密码   | 长度8-30，必须包含三项（大写字母、小写字母、数字、 ()`~!@#$%^&*-+=&#124;{}[]:;'<>,.?/ 中的特殊符号） | 
|           | Ehpc部署模式 | Tiny，Simple，Standard                                                   |
|           | 计算节点实例类型 | 可用区下可以使用的计算节点规格                                                        |
|           | 计算节点数量   | 计算节点数量, 可选值: 1-99                                                      |
|           | 登录节点实例类型 | 可用区下可以使用的登录节点规格                                                        |
|           | 管控节点数量   | 管控节点数量, 可选值: 1,2,4                                                     |
| EHPC集群用户配置 | 用户密码     | 长度8-30，必须包含三项（大写字母、小写字母、数字、()~!@#$%^&*-_+=\                            |{}[]:;'/<>,.?/中的特殊符号） |
|                | 用户名称     | 登录集群所用的用户名，默认为lammps                                                   |
| 网络配置      | 可用区      | ECS实例所在可用区                                                             |
|           | VPC ID   | 资源所在VPC                                                                |
|           | 交换机ID    | 资源所在交换机                                                                |

## 部署流程
1. 访问计算巢AutoDock Vina社区版[部署链接](https://computenest.console.aliyun.com/user/cn-hangzhou/serviceInstanceCreate?ServiceId=service-7ef89f7679cb4813b4a3)，按提示填写部署参数：
    ![image.png](2.png)

2. 参数填写完成后可以看到对应询价明细，确认参数后点击**下一步：确认订单**。
   ![image.png](3.png)

3. 确认订单完成后同意服务协议并点击**立即创建**
   进入部署阶段。
    ![image.png](4.png)

## 使用流程
### 步骤一：通过控制台连接集群
1. 登录[弹性高性能计算控制台](https://ehpc.console.aliyun.com)。
2. 在顶部菜单栏左上角处，选择地域。
3. 在左侧导航栏，单击**集群**。
4. 在**集群**页面，找到在计算巢部署好的目标集群，单击**远程连接**。
    <img src="5.png" height="700" align="bottom"/>

5. 在**远程连接**页面，输入集群用户名、登录密码和端口，单击**ssh连接**。

### **步骤二：提交作业**

本文通过模拟小分子配体和生物大分子受体相互作用的过程，预测配体与受体的结合模式和亲和力，模拟实现对药物的筛选。目前商业应用较广泛的Specs、Enamine和ChemDiv化合物库，均可提供大量配体模拟计算配体和给定受体的相互作用。由于不同配体之间没有依赖，因此可以大规模并行处理。本文同样适用于其它大批量、高并发处理需求的生物、医药等场景。

1. 下载并解压作业文件。

   1.下载作业文件。

>说明:如果集群中没有安装git，请先执行sudo yum install -y git安装git。

```
git clone https://code.aliyun.com/best-practice/022.git
```

   2.解压作业文件。

```
cd 022
tar xzvf vina-ehpcarrayjob.tar.gz
```

2. 修改配置文件。

```
cd vina-ehpcarrayjob
vim conf.txt
```

在conf.txt中，删除以下两行内容：

```
receptor = 1fkn_rgd.pdbqt
ligand = $file
```


3. 创建作业脚本，命名为vina.sh。

```
cd /home/vinatest
vim vina.sh
```

脚本内容如下：

```
#!/bin/bash

#PBS -N vina_job
#PBS -l nodes=1:ppn=2
#PBS -l walltime=00:10:00
#PBS -j oe
#PBS -v receptor="022/vina-ehpcarrayjob/1fkn_rgd.pdbqt",ligand="022/vina-ehpcarrayjob/test/ligand_1.pdbqt",config="022/vina-ehpcarrayjob/conf.txt"


cd $PBS_O_WORKDIR

ppn="$NCPUS"
cd $PBS_O_WORKDIR


vina --receptor $receptor --config $config  --ligand $ligand --out out.pdbqt --cpu $ppn
```

4. 提交作业。

```
qsub vina.sh
```

预期返回如下，表示生成的作业ID为0.scheduler。

```
0.scheduler
```

### **步骤三：查看作业结果**

1. 查看作业运行情况。

```
qstat -x 0.scheduler
```

预期返回如下，当返回信息中S为R时，表示作业正在运行中；当返回信息中S为F时，表示作业已经运行结束。

```
Job id            Name             User              Time Use S Queue
----------------  ---------------- ----------------  -------- - -----
0.scheduler       vina_job         vinatest          00:01:56 F workq 
```

2. 使用VNC可视化查看作业结果。

    1. 打开VNC。 控制台操作时系统会自动打开集群安全组 12016 端口。 

       1. 在[弹性高性能计算控制台](https://ehpc.console.aliyun.com)的左侧导航栏，单击**集群**。 

       2. 在**集群**页面，找到目标集群，单击**更多** &gt; **VNC**。

       3. 使用VNC远程连接可视化服务。具体操作，请参见[连接可视化服务](https://help.aliyun.com/zh/e-hpc/user-guide/use-vnc-to-manage-a-visualization-service#section-bf6-eyn-edu)。

    2. 在VNC窗口中，选择**Application&gt;System Tools&gt;Terminal**。

    3. 在Terminnal中执行以下命令，打开AutoDock Tools并加载作业结果。

      >/usr/local/bin/adt /home/vinatest/022/vina-ehpcarrayjob/1fkn_rgd.pdbqt /home/vinatest/out.pdbqt

    4. 在弹出的AutoDock Tools窗口中加载模型后，显示结果如下：
    
       <img src="6.png" height="800" align="bottom"/>
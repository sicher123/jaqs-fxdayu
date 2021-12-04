# jaqs-fxdayu:股票多因子策略研究和分析框架jaqs拓展包

## 介绍
在jaqs官方版本的基础上,重点改进和优化了股票多因子研究部分的功能,帮助使用者更方便的去设计/评估和分析因子表现,优化因子效果，进行因子组合研究．

主要包括:

### 基础：
- dataservice

对jaqs底层dataapi的一个高级封装，提供了一些常用数据的快捷查询方法——如K线、交易日历、指数成分信息、行业分类信息等。 

- dataview

可视为一个基于pandas的针对因子场景的数据库,方便因子的设计实现.jaqs_fxdayu改进了官方版本,提供更便捷灵活的因子数据查询和操作功能

- digger

单因子分析及绩效可视化.改进官方版本

- performance

因子选股研究中常用的绩效计算方法.改进官方版本

### 拓展：
- analysis

单因子多维度分析.从因子ic,因子收益,选股潜在收益空间三个维度给出因子评价.新增模块

- process

提供常用的因子处理操作，如去极值，中性化等.新增模块

- optimizer

提供因子参数优化功能.新增模块

- multi_factor

提供多因子处理和组合功能.新增模块

- dp

针对A股因子研究和交易分析场景,提供了常用的小工具,如查询历史的交易日,历史的行业分类表等.新增模块

- timingdigger

择时信号研究,通过TimingDigger,可以在设计完选股因子和事件后,加入简单的择时出场条件对因子进行进一步测试.支持设置止盈,止损等出场方式.新增模块

- hf_dataview

针对高频因子(bar级别)和事件设计的数据操作和信号计算模块，功能和Dataview一致.新增模块

## 安装和更新
### 依赖
该模块基于JAQS进行拓展，且只支持`python3`，需要安装：`jaqs>=0.6.11`

jaqs的安装可以参考[JAQS官方文档](http://jaqs.readthedocs.io/zh_CN/latest/install.html)

- 如果未安装过jaqs，从pip安装:
```bash
$ pip install jaqs
```

- 如果已安装过jaqs,进行更新:
```bash
$ pip install -U --no-deps jaqs
```

### 安装
```bash
$ pip install jaqs_fxdayu
```

### 更新
当有新版本发布时，使用以下命令更新
```bash
$ pip uninstall jaqs_fxdayu
$ pip install jaqs_fxdayu
```

## 使用
该模块主要分为两部分：

### 基础API：
基于jaqs项目的原有模块进行替换和拓展。
支持monkey_patch或直接从jaqs_fxdayu中导入。

以使用Dataview为例：

- monkey_patch:
```
import jaqs_fxdayu
jaqs_fxdayu.patch_all() # 需要放在任何import jaqs.* 之前

from jaqs.data import DataView

dv = DataView()

...
```

!!! Note
    该使用方法的好处是最大程度兼容原生JAQS的代码，方便迁移。

- 直接导入:
```
from jaqs_fxdayu.data import DataView

dv = DataView()

...
```

!!! Note
    该使用方法的好处是更为直观，且支持IDE的静态代码提示功能。

### 拓展API：
主要为独立开发，提供一些因子分析中常用，而jaqs中未实现的拓展功能。
使用方法主要是从jaqs_fxdayu模块中导入:
例如：
```python
from jaqs_fxdayu.research import Optimizer
```


### 文档
[详细文档地址](http://jaqs-fxdayu.readthedocs.io/zh_CN/latest/)

## 最新功能
### 2018/7/15

dataview添加财务数据时，允许指定财报类型

### 2018/7/2

TimingDigger/SignalDigger 支持根据group划分组内quantile

预处理因子/信号数据时,若传入group参数,quantile计算会在组内进行而非在全数据集上进行.

### 2018/6/9

TimingDigger-create_event_report方法新增进出场点位画图功能

新增hf_dataview-针对高频因子(bar级别)和事件设计的数据操作和信号计算模块，功能和Dataview一致.

### 2018/6/5
选股叠加择时研究(TimingDigger)新增功能,通过TimingDigger,可以在设计完选股因子和事件后,加入简单的择时出场条件对因子进行进一步测试.支持设置止盈，止损等出场方式.

### 2018/4/19
参数优化器(optimizer)新增功能,支持在待优化公式中调用自定义方法.

### 2018/4/19
新增process-mad,用于因子去极值.优化了行业市值中性化的算法效率.

### 2018/4/16
新增multi_factor-get_factors_ret_df,用于获取因子收益序列矩阵．同时，combine_factors新增基于最近一段时间的因子收益进行多因子加权组合的方法．

### 2018/4/11
新增dataview-refresh_data方法,可对数据集进行更新．

### 2018/3/26
新增dataservice文档.dataservice是对jaqs底层dataapi的一个高级封装，提供了一些常用数据的快捷查询方法——如K线、交易日历、指数成分信息、行业分类信息等。 

### 2018/3/26

新增模块dp,针对A股因子研究和交易分析场景，提供了常用的小工具，如查询历史的交易日，历史的行业分类表等

添加对performance模块的说明文档　performance:因子选股研究中常用的绩效计算方法


### 2018/3/20

作为单独模块发布，更新文档

### 2018/3/19 更新

新增dataview-fields可选字段查询方式，详见文档　dataview-fields可选字段查询方式

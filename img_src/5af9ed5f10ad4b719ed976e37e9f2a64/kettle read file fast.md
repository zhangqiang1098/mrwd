# kettle read file fast

&ensp;&ensp;&ensp;&ensp;TL数据库的数据来源大都是文本文件，那么大量与文件有关的操作就十分重要，其中最为重要就是文件快速解析入库,现在遇到的问题就是读取文件速度慢。（其实后期发现不是文件读取慢，是整个流程慢，尤其是数据入库慢，kettle方案前面数据流会被后面拖累，导致会越来越慢）


## 数据文件解析

&ensp;&ensp;&ensp;&ensp;文件解析入库常用的三个控件，第一个控件名为文本文件输入，第二个控件为csv文件输入，第三个控件为固定宽度文件输入

### 间隔符文件解析入库

&ensp;&ensp;&ensp;&ensp;间隔符是文件解析入库重要的一种方式，建议大家使用间隔符来加工数据，间隔符的选择会在其他章节中提到，咱不在本章节中提供。

&ensp;&ensp;&ensp;&ensp;间隔符文件常用的控件就是文本文件输入，csv文件输入，现在介绍一下两个区别，如果文本文件输入还是比较快的话，那么就不需要使用csv文件输入，如果输入比较慢的话，那么就需要使用csv文件输入，在csv控件中将“并行读取文件”空格点开，这样会比之前提高10%左右效率。
 
 &ensp;&ensp;&ensp;&ensp;文件解析入库中可以有一些其他的脚本，sql语句，这些脚本也可以复制步骤了，这样的话就是可以入库。
 

&ensp;&ensp;&ensp;&ensp;==上面是单个文件优化，如果多个文件的话，可以使用多进程来操作，只需要在step选择step copy次数就可以了==
 
 

### 固定字段长度文件入库

&ensp;&ensp;&ensp;&ensp;这个和间隔符文件解析入库类似


## 减少转换流程

&ensp;&ensp;&ensp;&ensp;一般而言，文本文件并不是一模一样的入到数据库中，中间有以下加工处理流程，如外国的时间值转换为"yyyymmdd hh24:mi:ss'，这样的话就需要在转换中添加其他控件来完成数据加工，这样的话就需要多进程操作,在某个节点效率转换特变慢时，可以使用多复制模式来提高效率，或者减少转换流程，这个转换流程某些可以到数据库来操作，就到数据库来操作，虽然会使数据库的压力变大，但是对于及时性而言，谁快谁是王道。


## 数据只插入不更新

&ensp;&ensp;&ensp;&ensp;文本文件类数据首要是入库，如果使用插入更新控件，随着数据量的不断增大，数据维护成本会越来越高，不建议文本类文件直接与数据进行插入更新操作。如果我们只是插入的话，就会增加我们的处理步骤，前期工作量比较大，但是考虑后面维护以及效率问题，建议直插入不更新

## 批量入库OR单条入库

&ensp;&ensp;&ensp;&ensp;明显就是批量入库，其实一种kettle自带的批量入库，另外一种是bulk data loading,建议使用第一种方式，第二种方式一般情况下都需要自己手动安装某些应用，来完成相关的操作。



## 硬件方面 

网络带宽，这个是我觉得是影响最大的一点，之前我的带宽是10m,后来虚拟机给我调整为100m后，我的速度比起之前快了一倍，目前对硬件方面也不是很理解，只能说上面一点。




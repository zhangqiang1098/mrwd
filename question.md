[TOC]

# QUESTION



​	问题时在学习工作生活中遇到的情况，建议都记录在这里，尤其是在图书馆或者其他没网的地方，建议将问题或者下步要求的事情记录下来。





|   日期   |                             问题                             |                           详细描述                           | 是否解决 |
| :------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :------: |
| 20180707 |      [r语言画出三角函数](20180707/R语言_sin(x)图像.md)       |  将cosx,sinx,tgx,ctgx,arcsinx,arccosx,arctgx,arcctgx画下来   |          |
| 20180720 | [pg子进程与spid关系](20180720/PG_TERMINATE_BACKEND_子进程关系.md) | 客户端访问pg成功后，父进程会folk一个子进程来处理客户端信息，那么与pg_terminate_backend(spid)的spid关系 |          |
| 20180722 | [有道云笔记大写字母文件转化为小写](20180805/解决有道云笔记迁移github上的图片链接问题.md) | 有道云笔记拷贝到github中，本地文件存储的图片或者附件的文件夹都是大写，而链接地址是小写 |          |
| 20180724 | [man psql没有出现提示文档](20180724/man_psql_no_manual_entry_for_psql.md) | man find出现提示文档，而man psql没有出现提示文档，需要在哪里配置，或者需要做什么 |    N     |
| 20180729 |   [pg savepoint作用用法](20180806/postgresql_savepoint.md)   |        savepoint在事务提到什么作用，他的用法又是什么         |          |
| 20180729 |      [rpm不同名称含义](20180729/rpm_noarch.rpm_src.rpm)      | 在package中出现了\*.noarch.rpm,\*.src.rpm,\*.rpm，这几种不同的后缀代表什么意思 |          |
| 20180730 | [linux 同时关闭一批服务器](20180803/LINUX_关闭_一批服务器.md) | 目前虚拟机云上的服务器20甚至更多，当关闭完应用时，想同时关闭服务器如何操作 |          |
| 20180801 |  [pg 索引字段更新不支持hot](20180807/pghot不是索引更新.md)   | 测试发现普通字段更新只要空间允许就会支持hot,但是索引字段更新就不会 |          |
| 20180802 |                linux 存储 多路径 udev asmlib                 | 光纤存储接到两台linux服务器上，多路径如何做，udev或者asmlib绑定设备好处坏处 |    N     |
| 20180803 |                         pg 函数三态                          |                 三态指的是什么？各自的特点？                 |    N     |
| 20180804 | [gp部署完后无法使用yum安装依赖包](20180808/gp部署yum坏了.md) |          gp部署完成，通过yum安装一个图像化界面报错           |          |
| 20180805 |       [postgres gprof目录](20180810/pg_gprof_目录.md)        |  gprof目录是怎么产生的？用途是什么？里面的文件是否可以删除   |          |
| 20180811 |                   linux 如何查看消失的进程                   |           进程在内存中消失了，历史记录是否还有信息           |    N     |
| 20180820 | [换电脑虚拟机无法使用](20180820/VIRTUALBOX_无法启动虚拟机.md) |               cpu开启虚拟化部分虚拟机无法启动                |    N     |
| 20180824 |    [pg去除字段特殊字符](20180824/pg_去除字段特殊字符.md)     |                   去除一个字段内的标点符号                   |          |
| 20180828 | [centos7 安装图形化](20180828/linux_centos7_install_desktop.md) |        图形化没有安装，后期启动后安装图形化依赖包失败        |          |
| 20180914 |                          mongo 集群                          |            mongo创建collection并没有在界面中找到             |    N     |
| 20180915 |                       mpp gds无法使用                        |                 gds启动后，报限制ip地址访问                  |          |
| 20180921 |             virtualbox添加新的网络Host Only网络              | win10每次更新后，virtualbox的host only都需要重建，但是可能之前的环境还被注册，只能注册为192.168.1.2 |    N     |
| 20180923 |                     virtualbox 网络设置                      |                     virtualbox 网络原理                      |    N     |
| 20181022 |  [kettle突然不执行](20181022/kettle_运行一段时间不执行.md)   |             一个方案执行到一个环节时就是无法执行             |    N     |
| 20181030 | [gpload delimiter](20181030/gpload_delimiter_character_choose.md) |    gpload只能使用一个分割符，那么那些字符不容易被使用到？    |    N     |
| 20181106 | [虚拟机因为vt-x/amd-v无法打开](20181106/virtualbox_not_open_machine_with_vt-x.md) |             vt-x/amd-v硬件加速在你的系统中不可用             |          |
| 20181107 | [datastage_not_load_library](20181108/ibm_datastage_not_load_library.md) |                dastage无法加载Oracle的依赖包                 |    N     |
| 20181115 | [greenplum source install](20181115/greenplum_open_source_install.md) |                  greenplum 5.1.20 集群安装                   |    N     |
| 20181117 |                     Oracle awr 生成分析                      |                     Oracle awr 生成 分析                     |    N     |
| 20181119 |                     Oracle awr 详细分析                      |                                                              |          |
| 20181122 |                 [Oracle 分区表多 无法查看]()                 |         oracle 分区表 分区多1096 无法查看表结构信息          |          |
| 20181127 | [centos 7 无法使用root 用户登录图形化界面](20181126/centos_7_graphical_interface_input_root_correct_password_not_login.md) | 在centos7服务器启动后，在图形化界面输入root密码，无法进入root环境，gpadmin无法进入gpamdin环境，而原先的admin用户可以进入admin图形化环境 |    N     |
| 20181128 |               gp 表每日入库3亿数据量表如何设计               |         greenplum 每日入库3亿数据量，这张表如何设计          |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |
|          |                                                              |                                                              |          |












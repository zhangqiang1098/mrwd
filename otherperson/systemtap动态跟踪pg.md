## 为什么要动态跟踪pg 

1.想清楚数据库内部运行的细节

2.想获取更多地信息

## systemtap可以获取到哪些信息

1.  进入或退出某个函数触发事件，执行相应程序
2.  打印函数堆栈
3.  打印函数入参，和出参

## 安装过程


```
1.安装systemtap
yum install systemtap systemtap-runtime

2.手动安装依赖的内核调试信息包
kernel-debuginfo
kernel-debuginfo-common
kernel-devel
下载地址：
http://debuginfo.centos.org/7/x86_64/

3.支持pg需要的编译参数
--enable-dtrace（静态探测点）

简单例子

--触发事件打印当前事件
stap -v -e 'probe process("/home/postgres/pg10.5/bin/postgres").mark("query-start") {println(gettimeofday_s())}'
 
--打印该函数的参数
stap -L 'process("/home/postgres/pg10.5/bin/postgres").mark("query-start")'

--打印函数堆栈
stap -v -e 'probe process("/home/postgres/pg10.5/bin/postgres").mark("query-start") {print_usyms(ubacktrace())}'

--enable-debug


```


## 详细语法细节

```
https://spacewander.gitbooks.io/systemtapbeginnersguide_zh/content/1_Introduction.html
```



## 怎么用systemtap跟踪pg呢


### insert表中有索引和没索引差距有多大

```
--创建表
create table have_index(id int);
create index on have_index(id);

--插入语句
insert into have_index select generate_series(1,1000000);
```
systemtap脚本如下

```
stap -v -DMAXSKIPPED=200000 -e '
global var1
global var2
probe process("/home/postgres/pg10.5/bin/postgres").function("ExecInsert").call {   
  var1[pid(),0] = gettimeofday_us()
}

probe process("/home/postgres/pg10.5/bin/postgres").function("ExecInsert").return {   
  var1[pid(),1] = gettimeofday_us()
  var2[1] <<< var1[pid(),1] - var1[pid(),0]
}

probe process("/home/postgres/pg10.5/bin/postgres").function("heap_insert").call {   
  var1[pid(),2] = gettimeofday_us()
}

probe process("/home/postgres/pg10.5/bin/postgres").function("heap_insert").return {   
  var1[pid(),3] = gettimeofday_us()
  var2[2] <<< var1[pid(),3] - var1[pid(),2] 
}

probe process("/home/postgres/pg10.5/bin/postgres").function("ExecInsertIndexTuples").call {   
  var1[pid(),4] = gettimeofday_us()
}

probe process("/home/postgres/pg10.5/bin/postgres").function("ExecInsertIndexTuples").return {   
  var1[pid(),5] = gettimeofday_us()
  var2[3] <<< var1[pid(),5] - var1[pid(),4]
 
}

probe process("/home/postgres/pg10.5/bin/postgres").function("setLastTid").call {   
  var1[pid(),6] = gettimeofday_us()
}

probe process("/home/postgres/pg10.5/bin/postgres").function("setLastTid").return {   
  var1[pid(),7] = gettimeofday_us()
  var2[4] <<< var1[pid(),7] - var1[pid(),6]
 
}

probe process("/home/postgres/pg10.5/bin/postgres").function("list_free").call {   
  var1[pid(),8] = gettimeofday_us()
}

probe process("/home/postgres/pg10.5/bin/postgres").function("list_free").return {   
  var1[pid(),9] = gettimeofday_us()
  var2[5] <<< var1[pid(),9] - var1[pid(),8]
 
}

probe timer.s(5) {
	if ( @count(var2[1]) > 0 ) {
		printf("time : %d \n",gettimeofday_s())
		printf("ExecInsert            us min: %d, max: %d, avg: %d, sum: %d, count: %d\n", @min(var2[1]), @max(var2[1]), @avg(var2[1]), @sum(var2[1]), @count(var2[1]) )  
		printf("heap_insert           us min: %d, max: %d, avg: %d, sum: %d, count: %d\n", @min(var2[2]), @max(var2[2]), @avg(var2[2]), @sum(var2[2]), @count(var2[2]) )
		printf("setLastTid           us min: %d, max: %d, avg: %d, sum: %d, count: %d\n", @min(var2[4]), @max(var2[4]), @avg(var2[4]), @sum(var2[4]), @count(var2[4]) )
		printf("list_free           us min: %d, max: %d, avg: %d, sum: %d, count: %d\n", @min(var2[5]), @max(var2[5]), @avg(var2[5]), @sum(var2[5]), @count(var2[5]) )
			if ( @count(var2[3]) > 0 ){
	    printf("ExecInsertIndexTuples us min: %d, max: %d, avg: %d, sum: %d, count: %d\n", @min(var2[3]), @max(var2[3]), @avg(var2[3]), @sum(var2[3]), @count(var2[3]) )
		}
		printf(" \n")
	}
}'
```

### 打印函数堆栈


```
stap -v -DMAXSKIPPED=200000 -e '
probe process("/home/postgres/pg10.5/bin/postgres").function("heap_insert").call {   
  print_usyms(ubacktrace())
}
'
```



### insert values(),(),()和copy的差距有多大，差别在哪些方面


```
create table test_copy (id int);

--insert插入
insert into test_copy values(1),(2),(3),(4),(5);

--copy导入
copy test_copy from '/home/postgres/test_copy.csv';
```

systemstap脚本

```
global var1
global var2
probe process("/home/postgres/pg10.5/bin/postgres").function("ExecInsert").call {   
  var1[pid(),0] = gettimeofday_us()
}

probe process("/home/postgres/pg10.5/bin/postgres").function("ExecInsert").return {   
  var1[pid(),1] = gettimeofday_us()
  var2[1] <<< var1[pid(),1] - var1[pid(),0]
}



probe process("/home/postgres/pg10.5/bin/postgres").function("heap_insert").call {   
  var1[pid(),2] = gettimeofday_us()
}

probe process("/home/postgres/pg10.5/bin/postgres").function("heap_insert").return {   
  var1[pid(),3] = gettimeofday_us()
  var2[2] <<< var1[pid(),3] - var1[pid(),2] 
}


probe process("/home/postgres/pg10.5/bin/postgres").function("heap_multi_insert").call {   
  var1[pid(),4] = gettimeofday_us()
}

probe process("/home/postgres/pg10.5/bin/postgres").function("heap_multi_insert").return {   
  var1[pid(),5] = gettimeofday_us()
  var2[3] <<< var1[pid(),5] - var1[pid(),4] 
}

probe process("/home/postgres/pg10.5/bin/postgres").function("CopyFromInsertBatch").call {   
  var1[pid(),6] = gettimeofday_us()
}

probe process("/home/postgres/pg10.5/bin/postgres").function("CopyFromInsertBatch").return {   
  var1[pid(),7] = gettimeofday_us()
  var2[4] <<< var1[pid(),7] - var1[pid(),6] 
}


probe timer.s(5) {
	if ( @count(var2[1]) > 0 ) {
		printf("time : %d \n",gettimeofday_s())
		printf("ExecInsert            us min: %d, max: %d, avg: %d, sum: %d, count: %d\n", @min(var2[1]), @max(var2[1]), @avg(var2[1]), @sum(var2[1]), @count(var2[1]) )  
		printf("heap_insert           us min: %d, max: %d, avg: %d, sum: %d, count: %d\n", @min(var2[2]), @max(var2[2]), @avg(var2[2]), @sum(var2[2]), @count(var2[2]) )
		if (@count(var2[2]) >0 ){
		printf("heap_multi_insert     us min: %d, max: %d, avg: %d, sum: %d, count: %d\n", @min(var2[3]), @max(var2[3]), @avg(var2[3]), @sum(var2[3]), @count(var2[3]) )
		printf("CopyFromInsertBatch   us min: %d, max: %d, avg: %d, sum: %d, count: %d\n", @min(var2[4]), @max(var2[4]), @avg(var2[4]), @sum(var2[4]), @count(var2[4]) )
		}
		
		printf(" \n")
	}
}

```

### gdb

```
https://github.com/hellogcc/100-gdb-tips/blob/master/src/index.md
```

### pg内部日志打出

```
elog(WARNING," ")
make && make install
pg_ctl restart
```


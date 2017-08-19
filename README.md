# lightweight-java-profiler

## 来源
> Fork of https://github.com/dcapwell/lightweight-java-profiler

    原始来源：https://code.google.com/p/lightweight-java-profiler/

***
## 编译
现在都是64位vm，直接给参数进行编译
> make BITS=64 all

***
### 编译参数
    在global.h文件中。首先是采样的频率，缺省是100次 每秒；另外是最大采样的线程栈，缺省3000，超过3000就忽略（对于复杂的应用明显不够） ；最后是栈的深度，缺省是128（对于调用层次深的应用调大）。

编译成功后，生成一个build-64/liblagent.so

***
## 加入agent
很简单，直接在你的启动命令上添加如下参数：-agentpath:path/to/liblagent.so[:file=name]。启动应用后，会在启动目录下生成trace.txt文件（缺省），该文件就是我们需要的采样数据。

***
## 生成火焰图
大神Brendan Gregg7已经帮你做好了，直接check大神的项目：
<pre>
git clone http://github.com/brendangregg/FlameGraph
cd FlameGraph
./stackcollapse-ljp.awk &lt; ../traces.txt | ./flamegraph.pl > ../traces.svg
</pre>
效果图截屏参考网上火焰图，真正火焰图指上去会显示栈信息，看火焰图，找到那些长条分析，基本上就有方向了。
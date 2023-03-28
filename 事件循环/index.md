#  浏览器
- 浏览器线程：
  - JS引擎线程
  - GUI渲染线程，与JS引擎线程互斥
  - 定时器触发线程
  - 事件触发线程
  - 异步http请求线程
#  浏览器中的Event loop
- 宏任务 微任务  
宏任务队列可以有多个，微任务队列只能有一个  
常见的宏任务：setTimeout、setInterval、script、UI rendering、I/O  
常见的微任务：promise.then promise.catch MutationObserver

- 一开始执行栈空,我们可以把执行栈认为是一个存储函数调用的栈结构，遵循先进后出的原则。micro 队列空，macro 队列里有且只有一个 script 脚本（整体代码）。


- 全局上下文（script 标签）被推入执行栈，同步代码执行。在执行的过程中，会判断是同步任务还是异步任务，通过对一些接口的调用，可以产生新的 macro-task 与 micro-task，它们会分别被推入各自的任务队列里。同步代码执行完了，script 脚本会被移出 macro 队列，这个过程本质上是队列的 macro-task 的执行和出队的过程。


- 上一步我们出队的是一个 macro-task，这一步我们处理的是 micro-task。但需要注意的是：当 macro-task 出队时，任务是一个一个执行的；而 micro-task 出队时，任务是一队一队执行的。因此，我们处理 micro 队列这一步，会逐个执行队列中的任务并把它出队，直到队列被清空。


- 执行渲染操作，更新界面


- 检查是否存在 Web worker 任务，如果有，则对其进行处理


- 上述过程循环往复，直到两个队列都清空
#  node事件循环
- 顺序：

外部输入数据 -> poll轮询阶段 -> check检查阶段 -> close callback 关闭事件回调阶段 -> timer 定时器检测阶段 -> I/O callbacks - I/O事件回调阶段 -> 闲置阶段 idle prepare -> ...轮询阶段



timer：执行setTimeout和setInterval回调，由poll阶段控制
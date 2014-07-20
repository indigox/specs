Promise 最佳实践
================
1. 链式任务一定要在回调中返回 promise 对象
2. 当不再有 then，也不再返回 promise 的时候一定记得 catch，并打印日志，良好的习惯可以明显提高调试效率
3. 可以在链式调用中间 catch 错误，并抛出 wrapped 异常，让异常更易读


两个 Promise 标准
=================

Promise/A+
----------
Sped  
<https://www.promisejs.org/>

Implementing
- promise  
  <https://github.com/then/promise>


Deferred
--------
Implementing
- jQuery.Deferred()  
  <http://api.jquery.com/category/deferred-object/>

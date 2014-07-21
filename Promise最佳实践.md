Promise 最佳实践
================
1. 链式任务一定要在回调中返回 promise 对象

        asyncGet(...)
          .then(function(data){
            return asyncUpdate(...);
          });

2. 当不再有 then，也不再返回 promise 的时候一定记得 catch，并打印日志，良好的习惯可以明显提高调试效率

        asyncGet(...)
          .then(function(data){
            console.log(data);
          })
          .catch(function(err){
            console.error(err);
          });

3. 可以在链式调用中间 catch 错误，并抛出 wrapped 异常，让异常更易读

        asyncGet(..) // get data1
          .catch(function(err){
            var wrap = new Error("Get data1 error.");
            wrap.inner = err;
            return Promise.reject(wrap);
          })
          .then(function(data){
            return asyncGet(...); // get data2
          })
          .catch(function(err){
            var wrap = new Error("Get data2 error.");
            wrap.inner = err;
            return Promise.reject(wrap);
          })
          .catch(function(err){
            console.error(err);
          });

4. 如何将一个普通的 promise 对象转成 angularjs $q 生成的 promise 对象

        $q.when(asyncGet(...))

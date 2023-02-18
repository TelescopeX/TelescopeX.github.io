---
# promise 解决回调地狱的问题

<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>回调地狱与promise</title>
</head>

<body>
  <script>

    ##先准备两个事件

    //获取奶茶的方法
    function getTea(fn) {
      setTimeout(() => {
        fn("喝奶茶")
      }, 500);
    }


    //获取火锅的方法
    function getHotpot(fn) {
      setTimeout(() => {
        fn("吃火锅")
      }, 1000);
    }

    ##先用回调地狱的方法按自己想要的顺序获取事件

    ###我们可以看出 因为"吃火锅"定时器事件比 "喝奶茶"定时器事件要长，
    ###所以"吃火锅"函数要将"喝奶茶"函数包裹在里面，如果继续增加就要层层嵌套形成了回调地狱，不方便维护。

    //调用获取火锅的方法

    getHotpot(((data) => {
      console.log(data);

      //调用获取奶茶的方法
      getTea(((data) => {
        console.log(data);
      }))
    }))  
 
 ##用promise的方法按自己想要的顺序获取事件

   ###先new一个 "喝奶茶" 的Promise，
    function getTea() {
      return new Promise(function (resolve) {
        setTimeout(() => {
          resolve("喝奶茶")
        }, 500)
      })

    }

    ###再new一个 "吃火锅" 的Promise，
    function getHotpot() {
      return new Promise(function (resolve) {
        setTimeout(() => {
          resolve("吃火锅")
        }, 1000);
      })
    }

    ###用 .then 的方法获取数据--链式操作

       getHotpot().then(function (data) {
         console.log(data); //这是吃火锅的数据

         return getTea()
       }).then(function (date) {
         console.log(date); //这是喝奶茶的数据
    
       }) */

    ###用async 函数调用 更精简，看起来像是同步的。
    async function getData() {

      //直接获取 resolve 传过来的数据
      let hotPot = await getHotpot(); //吃火锅
      console.log(hotPot);

      let Tea = await getTea(); //喝奶茶
      console.log(Tea);
    }

    //调用getData函数
    getData()

  </script>
</body>

</html>
---

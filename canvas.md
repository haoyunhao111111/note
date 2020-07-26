## API

1. canvas一定要把width和height写在canvas标签上，不能写在css样式里,在css里面会有拉伸

   ```html
   <canvas id='canvas' width='500' hieght='200'>对不起，你的浏览器版本过低，请升级</canvas>
   ```

   ```javascript
   // 得到元素标签
   let canvas = document.getElementById('canvas')
   // 上下文 -> 今后绘制所有的图形图片都是使用ctx,而不是使用canvas
   let ctx = canvas.getContext('2d') // 2d -> 在平面绘图
   ```

2. 绘制长方形

   ```javascript
   // 填充
   ctx.fillStyle = 'rgb(200,0,0)' // 填充颜色需要在绘制之前，否则会失效
   ctx.fillRect(0,0,100,300) // (x点坐标,y点坐标,宽,高)
   // 描边
   ctx.s  trokeStyle = 'rgb(200,0,0)'
   ctx.strokeRect(0,0,100,300)
   ```

3. 填充和描边

   1. canvas绘制，分为填充`fill`,描边`strocke`,基本形状`线`，`矩形`，`弧`

      1. 画线

         ```javascript
         ctx.beginPath() // 开始画线
         ctx.moveTo(0,0) // 从0,0点开始画线
         ctx.lineTo(100,100) // 在100,100点结束
         ctx.lineTo(0,100)
         ctx.lineWidth = '10' // 线宽
         ctx.strokeStyle = 'red'  // 线的颜色
         ctx.closePath() // 结束划线，将绘制的线段封闭
         ctx.stroke() // 将绘制的抽象的线段显示出来
         ctx.fillStyle = 'yellow' // 填充颜色
         ctx.fill()
         ```

      2. 画弧

         ```javascript
         // 圆心点x位置，圆心点y位置，半径大小，开始画的位置，结束位置，是否逆时针
         ctx.arc(100,100,100,0,2*Math.PI,true)
         ```

      3. 图片

         ```javascript
         let canvas = document.getElementById('canvas')
         let ctx = canvas.getContext('2d')
         let image = new Image()
         // 一旦设置src属性，将发出https请求
         image.src = 'C:/Users/hyh/Desktop/1/1.jpg'
         image.onload = function() {
             ctx.drawImage(image, 20, 20)  // ctx必须放在image.onload里面，因为读取图片是异步的操作
         }
         ```

         

      

      
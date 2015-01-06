# 程序3：有重力加速度的球 #

这个程序对应于 `NOC_2_1_forces.pde`，

我们绘制了一个有重力加速度的球。越下落速度越快，但接触地面时会反弹，由于重力作用，越上升速度越慢。

![程序运行截图](wind_gravity_forces.jpg)

点击按钮 _West Wind_ 对球施加从左吹来的风力作用。

可以从 <https://github.com/jollywing/nature_of_code_examples_html5/blob/master/chp2_forces/wind_gravity_forces.html> 下载该程序，用浏览器打开即可运行。

程序代码如下：

    <!doctype html>
    <html>
      <head>
        <title>Wind and Gravity force</title>
        <meta charset="utf-8" />
        <meta name="author" content="JollyWing(jiqingwu@gmail.com)"/>
        <meta name="create" content="2015-01-06 Tue"/>
        <style type="text/css">
         #screen {border:1px solid #000; margin-left:auto; margin-right:auto;}
         p.Scr {text-align:center;}
        </style>
        <script>
         // get context
         var scr;
         var ctx;
         var timeOut;

         var position = new Object();
         position.x = 5;
         position.y = 5;

         var velocity = new Object();
         velocity.x = 0;
         velocity.y = 0;

         var gravityAccel = new Object();
         gravityAccel.x = 0;
         gravityAccel.y = 1;

         var windAccel = new Object();
         windAccel.x = 1;
         windAccel.y = 0;

         var ball = {
           pos: position,
           radius: 5,
           vel: velocity,

           erase: function(){
             var top, left;
             //caculate the topleft
             left = this.pos.x - this.radius - 1;
             top = this.pos.y - this.radius - 1;
             // clear rect
             ctx.clearRect(left, top, this.radius*2 + 2, this.radius*2 + 2);
           },

           draw: function(){
             // set context property
             ctx.strokeStyle="red";
             ctx.fillStyle="yellow";
             // draw
             ctx.beginPath();
             ctx.arc(this.pos.x, this.pos.y, this.radius, 0, 2*Math.PI);
             ctx.stroke();
             ctx.fill();
           },

           checkEdge: function(){
             if(this.pos.x < 0){
               this.pos.x = this.radius;
               this.vel.x *= -1;
             }
             if(this.pos.x > scr.width){
               this.pos.x = scr.width - this.radius;
               this.vel.x *= -1;
             }
             if(this.pos.y < 0){
               this.pos.y = this.radius;
               this.vel.y *= -1;
             }
             if(this.pos.y > scr.height){
               this.pos.y = scr.height - this.radius;
               this.vel.y *= -1;
             }
           },

           addForce: function(accel){
             this.vel.x += accel.x;
             this.vel.y += accel.y;
           },

           move: function(){
             this.pos.x += this.vel.x;
             this.pos.y += this.vel.y;
           },
         };

         function initScr(){
           scr = document.getElementById('screen');
           ctx = scr.getContext('2d');
           ball.draw();
         }

         function updateScr()
         {
           // erase ball
           ball.erase();
           // add gravity force
           ball.addForce(gravityAccel);
           // update ball position
           ball.move();
           // check edges
           ball.checkEdge();
           // draw ball
           ball.draw();

           timeOut = setTimeout('updateScr()', 100);
         }

         function startWalk()
         {
           updateScr();
         }

         function stopWalk()
         {
           clearTimeout(timeOut);
         }

         function westWind()
         {
           // add wind force to velocity
           ball.addForce(windAccel);
         }
        </script>
      </head>
      <body onload="initScr()">
        <p class="Scr">
          <canvas id="screen" width="640" height="640"></canvas>
          <br/>
          <input type="button" value='Start' onclick='startWalk()'/>
          <input type="button" value='Stop' onclick='stopWalk()' />
          <input type="button" value="West Wind" onclick='westWind()'/>
        </p>
      </body>
    </html>

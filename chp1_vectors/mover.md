# 程序2：一直向前 #

这个例子里，描述了一个一直向前的对象。

每一次，对象会随机选一个出生位置和一个方向，然后一直运动下去。如果碰到边缘，就会转到画布的另一边继续沿原来的方向前进。

html5代码如下（可以从<https://github.com/jollywing/nature_of_code_examples_html5/blob/master/chp1_vectors/mover.html> 下载该文件）：

    <!doctype html>
    <html>
      <head>
        <title>Mover</title>
        <meta charset="utf-8" />
        <meta name="author" content="JollyWing(jiqingwu@gmail.com)"/>
        <meta name="create" content="2014-12-17 Wed"/>
        <style type="text/css">
         #screen {border:1px solid #000;}
        </style>
        <script>
         var mover = {
           /* x:100,
           y:100,
           xspeed:11,
           yspeed:10, */
           radius:2,
           init:function(canvasWidth, canvasHeight){
             this.x = Math.floor(Math.random() * canvasWidth);
             this.y = Math.floor(Math.random() * canvasHeight);
             this.xspeed = 1 + Math.floor(Math.random() * 10);
             this.yspeed = 1 + Math.floor(Math.random() * 10);
             console.log(this.xspeed + ',' + this.yspeed);
           },
    
           move:function(canvasWidth, canvasHeight){
             this.x = this.x + this.xspeed;
             this.y = this.y + this.yspeed;
    
             if(this.x > canvasWidth - this.radius){
               this.x = this.radius;
             }
             else if(this.x < this.radius) {
               this.x = canvasWidth - this.radius;
             }
             if(this.y > canvasHeight - this.radius){
               this.y = this.radius;
             }
             else if(this.y < this.radius) {
               this.y = canvasHeight - this.radius;
             }
           },
    
           draw:function(context){
             context.moveTo(this.x, this.y);
             context.arc(this.x, this.y, this.radius, 0, 2*Math.PI);
             context.stroke();
           }
         };
    
         var timeOut;
         var scr, width, height, context;
    
         function initScr(){
           scr = document.getElementById('screen');
           width = scr.width;
           height = scr.height;
           context = scr.getContext('2d');
           context.strokeStyle="red";
         }
    
         function walk(){
           mover.move(width, height);
           mover.draw(context);
           timeOut = setTimeout('walk()', 200);
           // console.log(mover.x + ',' + mover.y);
         }
    
         function stopWalk(){
           clearTimeout(timeOut);
         }
    
         function init(){
           initScr();
           mover.init(width, height);
         }
        </script>
      </head>
      <body onload='init()'>
        <p>
        <canvas id="screen" width="640" height="480"></canvas>
        </p>
        <input type="button" value='Start' onclick='walk()'/>
        <input type="button" value='Stop' onclick='stopWalk()' />
      </body>
    </html>

运行结果：

![始终朝一个方向][1]


  [1]: /download/01gJl9ZXQC7o

2014-12-17 周三

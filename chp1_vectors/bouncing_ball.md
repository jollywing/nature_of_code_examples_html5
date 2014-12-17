《代码本色：用编程模拟自然系统》是一本好书，一定要读一读。用编程模拟自然，是我一直以来都想做的事，也是我编程的热情所在。无奈自己的数学和物理知识越剩越少，所以心有余而力不足。现在这本书来了，学完这本书一定可以让自己过够瘾。

此书的纸板和电子版都很贵，但代码可以在 [图灵社区](http://www.ituring.com.cn/book/1292) 下载。不过代码是用很少有人熟悉的 `processing` 语言写的，于是决定自己用 `html5` 都实现一遍，并将代码托管在[GitHub](https://github.com/jollywing/nature_of_code_examples_html5)上。

之所以选择html5，是因为不需要额外的配置，只要有一个现代的浏览器就可以观看程序的运行。另一个原因，就是趁机学习一下html5。

先来第一个简单的吧： Bouncing Ball。顾名思义，这是一个弹来弹去的球。

下面是我用html5的实现，拷贝下列代码，保存为后缀为html的网页文件，用浏览器打开即可。

    <!doctype html>
    <html>
      <head>
        <title>random walker</title>
        <meta charset="utf-8" />
        <meta name="author" content="JollyWing(jiqingwu@gmail.com)"/>
        <meta name="create" content="2014-12-16 Tue"/>
        <style type="text/css">
         #screen {border:1px solid #000;}
        </style>
        <script>
         var x = 100;
         var y = 100;
         var xspeed = 11;
         var yspeed = 10;
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
    
           x = x + xspeed;
           y = y + yspeed;
    
           if(x > width - 2 || x < 2){
             xspeed = xspeed * -1;
           }
           if(y > height - 2 || y < 2){
             yspeed = yspeed * -1;
           }
    
           console.log(x + ',' + y);
    
           context.arc(x, y, 2, 0, 2*Math.PI);
           context.stroke();
    
           timeOut = setTimeout('walk()', 200);
         }
    
         function stopWalk(){
           clearTimeout(timeOut);
         }
        </script>
      </head>
      <body onload='initScr()'>
        <p>
        <canvas id="screen" width="640" height="480"></canvas>
        </p>
        <input type="button" value='Start' onclick='walk()'/>
        <input type="button" value='Stop' onclick='stopWalk()' />
      </body>
    </html>

下面是一个面向对象的版本：

    <!doctype html>
    <html>
      <head>
        <title>random walker</title>
        <meta charset="utf-8" />
        <meta name="author" content="JollyWing(jiqingwu@gmail.com)"/>
        <meta name="create" content="2014-12-16 Tue"/>
        <style type="text/css">
         #screen {border:1px solid #000;}
        </style>
        <script>
         var sprite = {
           x:100,
           y:100,
           xspeed:11,
           yspeed:10,
           radius:2,
           move:function(canvasWidth, canvasHeight){
             this.x = this.x + this.xspeed;
             this.y = this.y + this.yspeed;
    
             if(this.x > canvasWidth - this.radius || this.x < this.radius){
               this.xspeed = this.xspeed * -1;
             }
             if(this.y > canvasHeight - this.radius || this.y < this.radius){
               this.yspeed = this.yspeed * -1;
             }
    
           },
           draw:function(context){
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
           sprite.move(width, height);
    
           sprite.draw(context);
    
           timeOut = setTimeout('walk()', 200);
         }
    
         function stopWalk(){
           clearTimeout(timeOut);
         }
        </script>
      </head>
      <body onload='initScr()'>
        <p>
        <canvas id="screen" width="640" height="480"></canvas>
        </p>
        <input type="button" value='Start' onclick='walk()'/>
        <input type="button" value='Stop' onclick='stopWalk()' />
      </body>
    </html>

运行效果如图：

![弹来弹去][1]

-----------------

**如果你喜欢我的文章，可以点 [这里](http://weibo.com/p/1001603784418899696375) 给我打赏，五分一毛也是对我的认同。**
 


  [1]: /download/01gJiJhwoGK3

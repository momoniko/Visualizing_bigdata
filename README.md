# **大数据可视化展示学习笔记**

----

## **环境准备 + Echarts学习**

​	 1.vscode下载插件: cssrem （插件标准值设置为80px）
​		插件-配件按钮-配置扩展设备-Poot Font Size 里面设置
​		记得重新启动vscode
​	2.导入flexible.js把屏幕分为24份

​		下面为其代码：

```	javascript
(function flexible(window, document) {
  var docEl = document.documentElement;
  var dpr = window.devicePixelRatio || 1;

  // adjust body font size
  function setBodyFontSize() {
    if (document.body) {
      document.body.style.fontSize = 12 * dpr + "px";
    } else {
      document.addEventListener("DOMContentLoaded", setBodyFontSize);
    }
  }
  setBodyFontSize();

  // set 1rem = viewWidth / 10
  function setRemUnit() {
    var rem = docEl.clientWidth / 24;
    docEl.style.fontSize = rem + "px";
  }

  setRemUnit();

  // reset rem unit on page resize
  window.addEventListener("resize", setRemUnit);
  window.addEventListener("pageshow", function(e) {
    if (e.persisted) {
      setRemUnit();
    }
  });

  // detect 0.5px supports
  if (dpr >= 2) {
    var fakeBody = document.createElement("body");
    var testElement = document.createElement("div");
    testElement.style.border = ".5px solid transparent";
    fakeBody.appendChild(testElement);
    docEl.appendChild(fakeBody);
    if (testElement.offsetHeight === 1) {
      docEl.classList.add("hairlines");
    }
    docEl.removeChild(fakeBody);
  }
})(window, document);

```

  3. 导入Echarts.js库

     1. 下载：z在powershall或者cmd中 ，通过npm i echart下载

     2. 引入

        `<script src = "js/echart.min.js> </script>" 	`   

             		3.	初始化实例对象，将其放在dom（假设class=”main“,具备大小!）容器里面

        `var myChart = echarts.init(document.etElementById('.main')); `

             		4.	指定图表的配置项和数据（option）

        ![image-20201118200734157](C:\Users\Gzf\Desktop\个人文件\前端学习\image-20201118200734157.png)

             		5.	将配置项设置给Echarts实例对象

        `myChart.setOptio(option)`

  4. option配置扩展

     		1.	`title：{text："图标标题"}`
     		2.	`color:['red','blue','pink']`  //折线颜色
     		3.	`tooltip:{ trigger:'axis'} `   //图表提示框组件，里面为触发方式，提示点的内容
     		4.	`legend:{data:['例子','例子']}`   图例组件
     		5.	`toolbox:{ feature:{ saveAsImage:{}}}`  //工具箱组件，可以另存为图片等功能
     		6.	`grid:{left:'',right:'',bottom:'',containLabel:true}`   //网格配置，grid可以控制线形图、柱状图、图表大小，containLabel是否显示标签。
     		7.	`series：[{name:'名称',type:'类型',data:'[数据]'},{...},{...}]`  //系列图表配置，他决定这显示哪种类型的图标
     		8.	xAxis ：x坐标；yAxis：y坐标

------

## 具体操作

​	1.去官方选取模板

​	2.修改数据

​	3.官方网站寻找图表样式（文字、颜色、线条、柱子宽度）设置

-----

## 优化代码

​	1.立即执行函数

​		立即执行函数都是一个独立的函数，不会互相影响，即使里面的文字相同

​		在函数外面加个括号，例子如下：

```javascript
(function(){
	var myChart = echarts.init(document.querySelector(".bar",".chart"))
	......
})();
```

​	2.图表跟随窗口自适应

​		只需添加代码，如下

```javascript
window.addEventListener("resize",function(){
   maChart.resize(); 
})
```


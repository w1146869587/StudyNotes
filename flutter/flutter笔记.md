# flutter笔记

## 一、组件

## **1、MaterialApp**

1)、title 

String

2）、theme

ThemeData.dark()

3）、home 

Widget

## **2、Scaffold**

1)、appBar

AppBar

2)、body

Widget

3)、backgroundColor

Colors.blue

## **3、Text**

Text(

"this is text",

textDirection: TextDirection.ltr

)

## **4、floatingActionButton**

floatingActionButton: FloatingActionButton(

​    onPressed: _incrementCounter,

​    tooltip: 'Increment',

​    child: Icon(Icons.add),

   ), 

## **5、Text**

1)、textAlgin

文本对齐方式（center居中，left左对齐，right右对齐,justfy两端对齐）

2）、textDirection

文本方向（ltr从左至右，rtl从右至左）

3）、overflow 

文字超出屏幕之后的处理方式（clip 裁剪，fade渐隐，ellipsis省略号）

4）、textScaleFacotr 

字体显示倍率

5）、maxLines

文字显示最大行数

6）、style （TextStyle）

字体的样式设置

***下面是TextStyle的参数：***

- decoration

文字装饰线（none没有线，lineThrough删除线，overline 上划线，underline下划线）

- decorationColor

文本装饰线颜色

- decorationStyle

文字装饰线风格（【dashed,dotted】虚线，double两根线，solid一根实线，wavy波浪线）

- wordSpacig 

单词间隙（如果是负值，会让单词变得更紧凑）

- letterSpacing 

字母间隙（如果是负值，会让字母变得 列紧张紧凑）

- fontStyle

文字样式（italic斜体，normal正常体）

- fontSize

文字大小

- color

文字颜色

- fontWeight

字体粗细（bold粗体，normal正常体）

## **6、Container**

1)、alignment

topCenter:顶部居中对齐

topLeft：顶部左对齐

topRight:顶部右对齐

center:水平垂直居中对齐

centerLeft:垂直居中水平居左对齐

centerRight：垂直居中水平右对齐

bottomCenter:底部居中对齐

bottomLeft:底部居中左对齐

bottomRight:底部居右对齐 

2）、decoration

decoration:BoxDecoration(

​	color:Colors.blue,

​	border:Border.all(

​		color:Colors.red,

​		width:2.0,

​	),

​	borderRadius:BorderRadius.all(

​		Radius.circular(8.0)

   ),

);

3)、margin

margin属性是表示Container与外部其他组件的距离。

EdgeInsets.all(20.0),

4)、padding

padding就是Container的内边距，指Container边缘与Child之间的距离

pading:EdgetInsets.all(10.0)

5)、transform

让Container容易进行一些旋转之类的

transform:Matrix4.rotationZ(0.2)

6)、height

容器高度

7）、width

容器宽度

8）、child

容器子元素

（shorthand 简略表达式）


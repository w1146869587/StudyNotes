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

## ***注意：MediaQuery***

double rpx = MediaQuery.of(context).size.width / 750;

## **7、Row**

1)、mainAxisAlignment

 mainAxisAlignment: MainAxisAlignment.center,

2）、crossAxisAlignment

crossAxisAlignment: CrossAxisAlignment.center,

3）、children:

 children: <Widget>[]

## **8、Column**

1)、mainAxisAlignment

 mainAxisAlignment: MainAxisAlignment.center,

2）、crossAxisAlignment

crossAxisAlignment: CrossAxisAlignment.center,

3）、children:

 children: <Widget>[]

## **9、Padding**

1）、padding

padding:EdgeInserts.all(2.0);

2)、child

## **10、Image**

Image.asset     本地图片

Image.network 远程图片

1）、alignment 

Alignment

图片的对齐方式 

2)、color colorBlendMode

设置图片的背景颜色，通常和colorBlendMode配合一起使用，这样可以是图片颜色和背景色混合。 上面的图片主是进行了颜色的混合，绿色背景和图片红色的混合

3)、fit

BoxFit 

fit 属性用来控制图片的拉伸和挤压，这都是父容器来的。

BoxFit.fill：全图显示，图片会被拉伸，并充满父容器。

BoxFit.contain:全图显示，显示原比例，可能会有空隙。

BoxFit.Cover:显示可能拉伸，可能裁切， 充满（图片要充满整个容器，还不变形）。

BoxFit.fitWidth:宽度充满（横向充满），显示可能拉伸，可能裁切。

BoxFit.fitHeight:高度充满（竖向充满），显示可能拉伸，可能裁切。

BoxFit.scaleDown:效果和contain差不多，但是此属性不允许显示超过源图片大小，可小不可大。

BoxFit.scaleDown:效果和contain差不多，但是此属性不允许显示超过源图片大小，可小不可大。

4）、repeat

平铺

ImageRepeat.repeat 

横向和纵向都进行重复，直到铺满整个画布。 
ImageRepeat.repeatX

横向重复，纵向不重复。 

ImageRepeat.repeatY
纵向重复，横向不重复。 

5)、width                         
宽度  一般结合ClipOval才能看到效果 
6）、height      
高度  一般结合ClipOval才能看到效果 

## **11、SizedBox**

1)、width

2)、height

## **12、ListView**

1）、scrollDirection

Axis

Axis.horizontal 水平列表

Axis.vertical 垂直列表

2）、padding

EdageInset.all

内边距

3）、resolve

组件反射排序

4）、children

List<Widget>[]

列表元素

5)、ListView.builder

动态列表

ListView.builder(

​     itemCount: 119,

​     itemBuilder:(context,index){

​      return Container(

​       child: Text(

​        "$index"

​       ),

​      );

​     }, 

​    )

## 问题

>  If you are using a material widget component, like `Scaffold`, `Material`, you don't need to specify `textDirection` in your `Text` widget because `Directionality` is implicitly provided in these cases. So, a good solution would be to use:

## **13、GridView**


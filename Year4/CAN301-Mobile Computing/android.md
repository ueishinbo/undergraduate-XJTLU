## TextView

<img src="https://i.loli.net/2021/09/16/pmUFZcHVqeTLSoJ.png" alt="WX20210916-170319.png" style="zoom:50%;" />

TextView 中的layout_width有三种

* 

TextView中的text：设置文字。 （可以通过@string/**具体name**来引入）

TextView中的textColor："#00000000"

* 前两位代表透明度00为完全透明FF为完全不透明
* 3-4位代表红色
* 5-6位代表绿色
* 7-8位代表蓝色

TextView中的textStyle：设置字体风格，三个可选值：normal (无效果), bold (加粗), italic (斜体). 如果不设置的话就是normal

TextView中的textSize: 设置为sp可在不同手机上自适应大小 

TextView中的background：控件的背景颜色，可以理解为填充整个控件的颜色，可以是图片

TextView中的gravity：设置当前Textview在手机中的位置（居中，还是左对齐..)



实际开发中的文字，颜色要放在res/value对应的xml中

<img src="https://i.loli.net/2021/09/16/Aa1hQrwq4UKtz3l.png" alt="WX20210916-181352.png" style="zoom:80%;" />

### 带阴影的textview

1. shadowColor：设置阴影颜色，需要与shadowRadius一起使用
2. 设置阴影的模糊程度，设置为0.1就变为字体的颜色了，建议使用3.0
3. shadowDX：设置阴影在水平方向上的偏移，就是水平方向阴影开始的横坐标位置
4. shadowDy：设置阴影在树枝方向的偏移，就是竖直方向阴影开始的纵坐标位置

### 实现跑马灯效果的TextVIew

1. singleLine:内容为单行显示

2. focussable：是否可以获取焦点

3. focusablelnTouchMode：用于控制视图在触摸模式下是否可以聚焦

4. ellipsize：在哪里省略文本

5. marqueeRepeatLimit：字幕动画重复的次数

6. Clickable 设置点击的时候运行跑马灯效果，但在实际业务中我们一般要求程序一开始就自动进行跑马灯效果 

7. 让程序一运行就进行跑马灯效果

   1. 自定义类继承TextView

   <img src="https://i.loli.net/2021/09/16/ovmAkVZNgcbxdCF.png" alt="WX20210916-185907.png" style="zoom:80%;" />

   然后调用isFocused方法并把返回值设为true；

   其次把xml头改为自定义类![WX20210916-190100.png](https://i.loli.net/2021/09/16/o9ycNmArjz7f6h3.png)

   2. 最后一行加入<requestFocus/> <img src="https://i.loli.net/2021/09/16/mrtRfPvJ15hnOwy.png" alt="WX20210916-194931.png" style="zoom:50%;" />

## Button

1. Drawable: 饮用的Drawable位图
2. state_focused:是否获得焦点
3. state_pressed:控件是否被按下
4. state_enabled：控件是否可用
5. state_selected：控件是否被选择，针对有滚轮的情况
6. state_checked：控件是否被勾选
7. state_checkable：控件可否被勾选，

* 在新版本中如果想改变button的背景颜色不但需要调用background，还得需要在values/themes.xml的第三行最后加上.Bridge

<img src="https://i.loli.net/2021/09/17/5nrWdSNs9ox7Riv.png" alt="WX20210917-203907.png" style="zoom:80%;" />

* 但是现在点击没有效果（需要点击变颜色，松开恢复颜色的效果）。你得在下图所示的位置新建一个Drawable Resource<img src="https://i.loli.net/2021/09/17/UYD92JxuMOcXH5e.png" alt="WX20210917-204358.png" style="zoom:80%;" />

然后输入以下数据: 两个item一个是设置未点击时候的状态，一个是点击后的状态（根据state_pressed="true/false"来判断）

```xml
<?xml version=" 1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@drawable/ic_baseline_account_balance_24" android:state_pressed="true"/>
    <item android:drawable="@drawable/ic_baseline_accessibility_24" android:state_pressed="false"/>

</selector>
```

最后吧background的位置替换为

```xml
android:background="@drawable/btn_sellect"
```

* 实际上，可以把button看作3层
  * 最底层是background
  * 中间是text
  * 最上面是foreground

-----

* 第一步创建完项目以后点击activity_main进入xml

<img src="https://i.loli.net/2021/09/29/RZpthq54sN9FlrL.png" alt="WX20210929-001429@2x.png" style="zoom:50%;" />

* 第二步：先把xml文件改成如下所示

<img src="https://i.loli.net/2021/09/29/EMmOCZFnwA3cKxT.png" alt="WX20210929-002706.png" style="zoom:50%;" />



### 设置button点击按钮显示不同的状态

**但此时Button点击没有任何反应，如果你想设置点击时候是一个状态，结束后又是一个状态,方法如下**

* 第一步：先创建一个Drawable文件,（命名随意，root element 选择selest）

<img src="https://i.loli.net/2021/10/06/IqB9s2aOwUiHdep.png" alt="WX20211006-110032@2x.png" style="zoom:50%;" />

* 创建两个状态（也就是默认状态，和点击时候的状态）<img src="https://i.loli.net/2021/10/06/qbojJhvGSV6zaXW.png" alt="WX20211006-110540@2x.png" style="zoom:50%;" />
  * 1是默认状态，2是点击状态。这个图片是导入进去的，导入方法如下
  * <img src="https://i.loli.net/2021/10/06/l2OcMDXIsTftCE5.png" alt="WX20211006-111021@2x.png" style="zoom:33%;" />
  * 选完图片以后一直点next就行了<img src="https://i.loli.net/2021/10/06/lyAavIibYQKh6mX.png" alt="WX20211006-111213@2x.png" style="zoom:33%;" />
  * 然后把这两个名字写入到item里
  * 最后再设置状态一个true(按下为true） 一个false<img src="https://i.loli.net/2021/10/06/vcP2HZJmk6MLYWj.png" alt="WX20211006-111719@2x.png" style="zoom:33%;" />



最后一步：把main里面的background设置为刚才的drawable文件即可

<img src="https://i.loli.net/2021/10/06/E9kNq8aojdv7IXi.png" alt="WX20211006-112137@2x.png" style="zoom:50%;" />

### 设置button点击时候不同颜色

颜色可以通过backgroundTint来设置，如果只设置一种颜色的话就永远是这个颜色，无论点击与否都一样，所以我们要写drawable的颜色选择器来控制它的颜色。

<img src="https://i.loli.net/2021/10/06/BOcWApq16JoXZbi.png" alt="WX20211006-113217@2x.png" style="zoom:50%;" />

* 第一步:创建一个颜色管理文件夹：<img src="https://i.loli.net/2021/10/06/BaKTlLdSzo2DRn7.png" alt="WX20211006-114327@2x.png" style="zoom:50%;" />

然后写下默认是绿色按下是红色

<img src="https://i.loli.net/2021/10/06/1oZOHdQXqTGkm36.png" alt="WX20211006-114628@2x.png" style="zoom:50%;" />

最后一步把backgroundTint内容改为刚才的选择器

<img src="https://i.loli.net/2021/10/06/h7MW6fosvrej2mU.png" alt="WX20211006-115119@2x.png" style="zoom:50%;" />

### Button事件处理

点击事件

长按事件

触摸事件

#### 第一步：

新建一个id

<img src="https://i.loli.net/2021/10/11/9WiH8FZcCMSOmAg.png" alt="WX20211011-142730@2x.png" style="zoom:50%;" />



#### 第二步：

切换到java代码并添加以下代码：

![WX20211011-152403@2x.png](https://i.loli.net/2021/10/11/OY3L8ZJevEVlFBT.png)

每个方法都有回调函数

#### 第三步：调试

![WX20211012-234441@2x.png](https://i.loli.net/2021/10/12/yxrlbcBe6L73Hj5.png)

```java
//点击事件
btn.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Log.e(TAG, "onclick: ");
    }
});

//长按事件
btn.setOnLongClickListener(new View.OnLongClickListener() {
    @Override
    public boolean onLongClick(View view) {
        Log.e(TAG, "onLongClick");
        return false;
    }
});

//触摸事件
 btn.setOnTouchListener(new View.OnTouchListener() {
     @Override
     public boolean onTouch(View view, MotionEvent motionEvent) {
         Log.e(TAG, "onTouch");
         return false;
     }
 });
```

也就是没个方法里加上Log.e()的方法。

**当轻点button的时候会执行触摸事件和点击事件。先执行触摸事件再执行点击事件**

**当长按button 的时候会执行上面全部事件，按住不动先执行长按事件，松手后执行触摸最后是点击事件**

## EditText

1. android:hint 输入提示
2. android:textColorHint 输入提示文字的颜色
3. android:inputType 输入类型
4. android:drawableXxxx 在输入框的指定地方添加图片
5. android:drawablePadding 设置图片与输入内容的间距
6. android:paddingXxxx 设置内容与边框的间距
7. android:backkground 背景色



### 测试hint,textColorHint,inputType 

测试前三个

<img src="https://i.loli.net/2021/10/13/3VtfZsmbMrL6wao.png" alt="WX20211013-153745@2x.png" style="zoom:67%;" />

<img src="https://i.loli.net/2021/10/13/xTcoWBupDK5dnYk.png" alt="WX20211013-153844@2x.png" style="zoom:50%;" />

### 测试drawableXxxx，

#### 第一步创建图片

<img src="https://i.loli.net/2021/10/13/7pmsdafWjyDlMJX.png" alt="WX20211013-160011@2x.png" style="zoom:50%;" />



然后选择一个图片，点next和finish完成。

<img src="https://i.loli.net/2021/10/13/gVWS3I2xjOUs6Ff.png" alt="WX20211013-160219@2x.png" style="zoom:50%;" />

### 测试android:drawablePadding 设置图片与输入内容的间距



然后加上红框内的代码，双引号里面填写刚才添加图片的路径。就会在text旁边显示刚才的图片，如图中右侧红框所示。

如果你觉的文字和图片之间太近了，可以加上如下红框内的代码可以增大间距。

<img src="https://i.loli.net/2021/10/13/GlrFzTJHdVWMR4S.png" alt="WX20211013-161042@2x.png" style="zoom:50%;" />

### android:paddingXxxx 设置内容与边框的间距

如果你觉的整个文本框里屏幕左边太近了，你可以用paddingLeft来设置。右边将就paddingRight设置。

### android:backkground 背景色

<img src="https://i.loli.net/2021/10/13/hKwCRHjJyGoAXOp.png" alt="WX20211013-162454@2x.png" style="zoom:50%;" />

这个黑色的线非常难看，所以你可以用background = white来清除这条线。

### 通过button获取text值

第一步先创建一个新的button,并给其加上id，再把一个textfield加上id

<img src="https://i.loli.net/2021/10/13/QMSVp7R6rzksd1y.png" alt="WX20211013-163810@2x.png" style="zoom:30%;" />

然后切换到java代码当中，  

![WX20211013-203047@2x.png](https://i.loli.net/2021/10/13/Tz7suBKryMbtdAp.png)

1:代表的是获取到button控件

2:代表的是获取button控件

3:代表的是打印出当点击按钮的时候，打印text的文本内容。

## Imagewiew

 ## ProgressBar

1. andorid:max : 进度条最大值
2. Android：progress： 进度条已完成进度
3. android: indeterminateminate: 如果设置为true，则进度条不精确显示
4. style："?android:attr/progressBartyleHorizontal" 水平进度条







Glide: 一种图片加载技术，可以填写本地或者http端的图片。可以设置占位符，如果图片加载失败显示别的图片。可以设置加载动画效果。

Okhttp和Retrofit 网络加载框架



Gson是用来操作json的 一个库 



RX开发思维模式，只注重开始和结果 



数据存储：

​	1. SP 存配置信息等，比如记住我，和自动登录、  








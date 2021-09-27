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
<?xml version="1.0" encoding="utf-8"?>
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





























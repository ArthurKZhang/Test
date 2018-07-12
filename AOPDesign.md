##1. 日志 
####1.1.  对方法 参数和返回值的打印
####1.2. 类成员变量值的跟踪
自定义注解 
```
@Logging{
作用域 METHOD+FIELD
String Tag 
int type log类型，默认debug
String traceName Trace打印的输出文件的名字
}
```

针对方法，参数和返回值默认打印，会记录方法运行时间和产生Trace输出。
针对类成员变量，每次成员变量被赋值都会输出一条log，**但是**意义不大，因为很多情况下对象一旦被赋值其引用不再变，变的是兑现的内容。例如 
```
Map m = new HashMap(...)
Map.put(......)
```
这种情况第二句不能引起m打印log。

##2. 性能监控
####2.1. 方法耗时-->日志已满足
####2.2. 出入参数打印-->日志已满足
####2.3. Trace-->日志已满足
####2.4. 页面加载耗时
针对性能监控的页面加载耗时检测，给出自定义注解
```
@PageLoadTime{
作用域 类
String Tag 
int type  log类型，默认debug
}
```
针对Activity 和 Fragment, 跟踪Activity和Fragment的生命周期中的回调方法来进行耗时计算。**但是**，Activity和Fragment类中需要显示的出现相应的方法，即必须要override方法。 
#####1. Activity类中必须存在两个方法：
```
@override onCreate()
@override onWindowFocusChanged()
```
#####2. Fragment类中必须存在两个方法：
```
@override onCreate()
@override onResume()
```


##3. 动态权限检查
自定义注解
```
@CheckPermission{
作用域METHOD, TYPE
String[] permissions  需要的权限数组，默认""空
String rationalMessage 合理性解释，默认""空
int rationalMsgResId() default 0;
String deniedMessage() default ""; 权限禁止显示内容
int deniedMsgResId() default 0;
String grantBtnMsg() default "同意";
int grantBtnMsgId() default 0;
String denyBtnMsg() default "取消";
int denyBtnMsgId() default 0;
boolean needGotoSetting() default false;是否去系统设置
boolean runIgnorePermission() default false;是否无视权限继续方法
}
```


##4. 代码异常保护
自定义注解
```
@HandleException{
作用域METHOD
boolean isCatch 拦截exception与否，默认false不拦截
String Tag
String Msg catch到exception时打印的log信息
}
```
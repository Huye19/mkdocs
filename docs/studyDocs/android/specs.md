# Android 代码规范

## 1 前言

### 1.1 目的说明

- 统⼀一编码标准，提⾼高开发效率
- 使代码通俗易易懂，更更易易于后期维护



## 2 命名规范

### 2.1 包

- 基础规则：小写、单词间连续无间隔、反域名法（分为4级，具体如下图）



![1](https://ask.qcloudimg.com/http-save/yehe-1001569/73faf22b7db4c536cca657ec7ae46c62.png)



- 第4级包名会随着功能的不同而不同。下面我列举出一些常见 & 需要规范的4级功能包名



![2](https://ask.qcloudimg.com/http-save/yehe-1001569/714f07d5a985d7826619d46b2e3ba065.png)



### 2.2 类

- 基础规则    

1. 类型 = 名词 / 名词短语；
2. 形式 = 驼峰形式中的大骆驼拼写法



- 在具体命名类时，会根据 **该类的类型不同而附加额外的命名规则**。具体如下图



![3](https://ask.qcloudimg.com/http-save/yehe-1001569/6e9c6aef2850243ae6358ba4882f0291.png)



### ~~2.3 变量~~

- 基础规则    

1. 类型 = 名词 / 名词短语；

2. 形式 = 驼峰形式中的 **小骆驼拼写法**

   
   

- 在具体命名变量时，会根据**该变量的类型不同而 附加额外的命名规则**。具体如下图



![4](https://ask.qcloudimg.com/http-save/yehe-1001569/796761a15767383ff1ee022ed6c89d3f.png)



### 2.4 方法

- 基础规则    

1. 类型 = 动词 / 动词短语；
2. 形式 = 驼峰形式中的 **小骆驼拼写法**



- 在具体命名 方法名时，会根据 **该方法名的作用不同而 附加额外的命名规则**。具体如下图



![5](https://ask.qcloudimg.com/http-save/yehe-1001569/f5ea1d9b7d22ac78445000aedfa3aab5.png)



### 2.5 参数名

- 基础规则：驼峰形式中的 **小骆驼拼写法**

- 附加命名规则：功能名，如`userName`



### 2.6 资源

- Android的资源包括:



![6](https://ask.qcloudimg.com/http-save/yehe-1001569/25c9bdbf30832693963d3692d2b1bc57.png)



![7](https://ask.qcloudimg.com/http-save/yehe-1001569/e0ae40e16d45b49e49c4ebf4dc1aad3b.png)



下面，我将对每种`Android`资源的命名规则进行详细讲解



#### 2.6.1 布局文件资源

![8](https://ask.qcloudimg.com/http-save/yehe-1001569/3758a07687e95932c7f5116b030172f0.png)



#### 2.6.2 图片资源

![9](https://ask.qcloudimg.com/http-save/yehe-1001569/430cd6ce8d57a1dfbe2afebe84ce7195.png)



![image-20240307201838439](/Users/huye/Library/Application Support/typora-user-images/image-20240307201838439.png)







#### 2.6.3 参数值资源

![9](https://ask.qcloudimg.com/http-save/yehe-1001569/49b5cc4dbde743470526ffa2a4a8fb51.png)



#### 2.6.4 动画资源

![10](https://ask.qcloudimg.com/http-save/yehe-1001569/94519de5f6528aa8d7f8d0853b2ba8dc.png)



#### 2.7 通用

![11](https://ask.qcloudimg.com/http-save/yehe-1001569/543b1e1069c038dd4dbbd0925e134258.png)

## 3 编码规范

### 3.1 换行策略

#### 3.1.1 操作符的换行

除赋值操作符之外，我们把换行符放在操作符之前，例如：

```
int longName = anotherVeryLongVariable + anEvenLongerOne - thisRidiculousLongOne
        + theFinalOne;
```

赋值操作符的换行我们放在其后，例如：

```
int longName =
        anotherVeryLongVariable + anEvenLongerOne - thisRidiculousLongOne + theFinalOne;
```



#### 3.1.2 多参数的换行

当一个方法有很多参数或者参数很长的时候，我们应该在每个 `,` 后面进行换行。

比如：

```
loadPicture(context, "https://blankj.com/images/avatar.jpg", ivAvatar, "Avatar of the user", clickListener);
```

我们应该使用如下规则：

```
loadPicture(context,

        "https://blankj.com/images/avatar.jpg",
        ivAvatar,
        "Avatar of the user",
        clickListener);

```



#### 3.1.3 RxJava链式的换行

RxJava 的每个操作符都需要换新行，并且把换行符插入在 `.` 之前。

```
public Observable<Location> syncLocations() {

    return mDatabaseHelper.getAllLocations()
            .concatMap(new Func1<Location, Observable<? extends Location>>() {
                @Override
                 public Observable<? extends Location> call(Location location) {
                     return mRetrofitService.getLocation(location.id);
                 }
            })
            .retry(new Func2<Integer, Throwable, Boolean>() {
                 @Override
                 public Boolean call(Integer numRetries, Throwable throwable) {
                     return throwable instanceof RetrofitError;
                 }
            });
}
```



### 3.2 编写简短方法

- 每行不超过 160 个字符。
- 在可行的情况下，尽量编写短小精炼的方法。我们了解，有些情况下较长的方法是恰当的，因此对方法的代码长度没有做出硬性限制。如果某个方法的代码超出 40 行，请考虑是否可以在不破坏程序结构的前提下对其拆解。



### 3.3 类成员的顺序

推荐使用如下排序：

1. 常量
2. 静态变量
3. 静态方法
4. 字段
5. 构造函数
6. 重写函数和回调
7. 公有函数
8. 私有函数
9. 内部类或接口



```
public class MainActivity extends Activity {

		// 常量
    private static final String TAG = MainActivity.class.getSimpleName();
    
		// 字段
    private String mTitle;
    private TextView mTextViewTitle;
		//重写函数
    @Override
    public void onCreate() {
        ...
    }
		// 公有函数
    public void setTitle(String title) {
        mTitle = title;
    }
		// 私有函数
    private void setUpView() {
        ...
    }
		// 内部类
    static class AnInnerClass {

    }
}

```



### 3.4 函数参数排序

在 Android 开发过程中，`Context` 在函数参数中是再常见不过的了，我们最好把 `Context` 作为其第一个参数。

正相反，我们把回调接口应该作为其最后一个参数。



```
// Context always goes first

public User loadUser(Context context, int userId);

// Callbacks always go last
public void loadUserAsync(Context context, int userId, UserCallback callback);

```





## 4 注释规范

### 4.1 类注释

- 每个类应包含作者、创建日期和简要描述。

```
/**
 * @author 创建人： XXX
 * @createTime 创建时间： 2022/6/28
 * @describe 描述：APP主界面
 * @email 邮箱：199999999XX@163.com
 */
 public class MainActivity {
 }

```



### 4.2 方法注释

- 每个方法应包含描述、参数说明和返回值说明。

```
/**
 * 获取在线设备名称
 * 
 * @param deviceList 设备列表
 * @param position 下标
 * @return 设备名称
 */
private String getOnlineDeviceName(ArrayList<DeviceInfo> deviceList， int position){
	... // 其他逻辑
	return deviceList.get(position).name;
}
```



### 4.3 区块注释

```
private void run(){
 // 单行注释
	xxx();
}


 private void run(){
 /*
 * 多⾏注释
 * /
 xxx();
 }
```



### 4.4 变量注释

```
 /**
 * 是否启动自动进入
 */
public static final String IS_CHANGE_FROM_START = "is_change_from_start";
```



## 5 代码提交

1.未经测试的代码，禁⽌提交，确保提交的代码不影响其他⼈正常开发流程

2.代码提交之前，必须先fetch并rebase，合并⾄最新代码后再push

3.提交 commit 规范为：

1 [需求] 需求名称以及内容

2 [集成] 变动SDK名称

3 [优化] 优化功能点

4 [修复] 修复bug内容

## 6 其他规范

### 6.1 常规规范

- 多打 Log 日志，便便于定位运行流程 
- 提交代码前，去掉或注释无关代码
- 方法的行数过长（大于50行）时，尽量拆分为多个子函数
- 主函数中尽量简洁、尽量不包括具体逻辑 
- 每行代码必须以分号结束
- 使用 **0px** 代替 **0dp**，这样就可以在获取时避免系统进行换算，提升代码的执行效率。
- 字符串比较，应该用 `"xxx".equals(object)`，而不应该用 `object.equals("xxx")`，因为 **object** 对象可能为空，我们应该把不为空的条件放置在表达式的前面。
- 字符串类型转换，应该用 `String.valueOf(Object object)` 来代替 `object.toString()`，因为 `object` 对象可能会为空， 直接调用 `toString` 方法可能会触发 `NullPointerException`，而 `valueOf` 方法内部有做判空处理。
- **long** 类型的常量应该以大写英文 **L** 结尾，而不应该用小写英文 **l**，因为小写英文的 **l** 会和数字 **1** 容易造成一些混淆，例如 **1l** 会被看成 **11**，而使用 **1L** 就不会出现这种情况。
- 尽量采用 **switch case** 来判断，如果不能实现则再考虑用 **if else**，因为在多条件下使用 **switch case** 语句判断会更加简洁。
- 严禁用 **switch case** 语句来判断资源 id，因为 Gradle 在 5.0 之后的版本，资源 ID 将不会以常量的形式存在，而 **switch case** 语句只能判断常量，所以不能再继续使用 **switch case** 来判断资源 ID 了。
- 不推荐用 **layout_marginLeft**，而应该用 **layout_marginStart**；不推荐用 **layout_marginRight**，而应该用 **layout_marginEnd**，原因有两个，一个是适配 Android 4.4 **反方向特性**（可在开发者选项中开启），第二个是 XML 布局中使用 **layout_marginLeft** 和 **layout_marginRight** 会有代码警告，**padding** 属性也是同理，这里不再赘述。另外有一点需要注意：严禁 **Left、Right** 属性和 **Start、End** 属性同时使用，两者只能二选一。
- 如果在 **layout_marginStart** 和 **layout_marginEnd** 的值相同的情况下，请替换使用 **layout_marginHorizontal**，而 **layout_marginTop** 和 **layout_marginBottom** 也同理，请替换使用 **layout_marginVertical**，能用一句代码能做的事不要写两句，**padding** 属性也是同理，这里不再赘述。
- **过期** 和 **高版本** 的 API 一定要做对应的兼容（包含 Java 代码和 XML 属性），如果不需要兼容处理的，需要对警告进行抑制。
- 在能满足需求的情况下，尽量用 **invisible** 来代替 **gone**，因为 **gone** 会触发当前整个 View 树进行重新测量和绘制。
- **api** 和 **implementation**，在能满足使用的情况下，优先选用 **implementation**，因为这样可以[减少一些编译时间](https://www.jianshu.com/p/8962d6ba936e)。
- **ListView** 和 **RecyclerView** 都能实现需求的前提下，优先选用 **RecyclerView**，具体原因不解释，大家应该都懂。
- **ScrollView** 和 **NestedScrollView** 都能实现需求的前提下，优先选用 **NestedScrollView**，是因为 **NestedScrollView** 和 **RecyclerView** 支持相互嵌套，而 **ScrollView** 是不支持嵌套滚动的。
- 不能在项目中创建副本文件，例如创建 `HomeActivity2.java`、`home_activity_v2.xml` 类似的副本文件，因为这样不仅会增加项目的维护难度，同时对编译速度也会造成一定的影响，正确的做法应该是在原有的文件基础上面修改，如果出现需求变更的情况，请直接使用 **Git** 或者 **SVN** 进行版本回退。
- 如果一个类不需要被继承，请直接用 **final** 进行修饰，如果一个字段在类初始化过程中已经赋值并且没有地方进行二次赋值，也应当用 **final** 修饰，如果一个字段不需要被外部访问，那么需要用 **private** 进行修饰。
- 时间间隔的计算，对于前后时间的获取，不推荐使用 `System.currentTimeMillis()` 来获取，因为用户随时可能会调整手机的日期，这样会导致计算出来的时间间隔不准确，推荐使用 `SystemClock.uptimeMillis()` 来获取，此 API 用于获取本次已开机的毫秒数，用户就算调整了手机的日期也没有任何影响；值得一提的是，**Handler** 类中的 `postDelayed` 方法也是采用这种方式实现。
- 每个小组成员应当安装[阿里巴巴代码约束插件](https://plugins.jetbrains.com/plugin/10046-alibaba-java-coding-guidelines)，并及时地对插件所提示的**代码警告**进行处理或者抑制警告。



### 6.2 后台接口规范

- 后台返回的 **id 值**，不要使用 **int** 或者 **long** 类型来接收，而应该用 **string** 类型来接收，因为我们不需要对这个 **id 值**进行运算，所以我们不需要关心它是什么类型的。
- 后台返回的**金额数值**应该使用 **String** 来接收，而不能用**浮点数**来接收，因为 **float** 或者 **double** 在数值比较大的情况下会容易丢失精度，并且还需要自己手动转换出想要保留的小数位，最好的方式是后台返回什么前端就展示什么，而到了运算的时候，则应该用 **BigDecimal** 类来进行转换和计算，当然金额在前端一般展示居多，运算的情况还算是比较少的。
- 我们在定义后台返回的 Bean 类时，不应当将一些我们没有使用到的字段添加到代码中，因为这样会消耗性能，因为 Gson 是通过**反射**将后台字段赋值到 Java 字段中，所以我们应当避免一些不必要的字段解析，另外臃余的字段也会给我们排查问题造成一定的阻碍。
- 如果后台给定的字段名不符合代码命名的时候，例如当遇到 `student_name` 这种命名时，我们应当使用 Gson 框架中的 **@SerializedName** 注解对字段进行映射。
- 请求的接口参数和返回字段必须要写上注释，除此之外还应该备注对应的后台接口文档地址，以便我们后续能够更好地进行维护和迭代。
- 后台返回的 Bean 类字段不能直接访问，而应该通过生成 **Get** 方法，然后使用这个 **Get** 方法来访问字段。
- 接口请求成功的提示可以不显示，但请求失败的提示需要显示给到用户，否则会加大排查问题的难度，也极有可能会把问题掩盖掉，从而导致问题遗留到线上去。
- 如果用的 Json 解析框架是 Gson，则建议进行容错处理，秉持不信任后台的原则，因为我们没有办法控制后台返回了什么数据结构，但是我们有办法保证应用不会为这个问题而导致崩溃。



6.3 

1.XML布局中尽量减少层级。

2.布局控件数量⼤于10个时，使⽤ConstraintLayout，否则使⽤其他Layout，考虑使⽤优先级：

FrameLayout>LinearLayout>RelativeLayout>其他。

RecyclerViewHolder的布局⽂件中，不要使⽤ConstraintLayout。

3.布局⽂件中，TextView的text属性，禁⽌直接写死字符串，必须添加@string引⽤

// 4.使⽤AppCompatXXXView代替XXXView（暂不做要求）

5.同属性超过4个时，需要使⽤style

6.及时删除多余import及代码格式化，每次编码完成后习惯性Ctrl+Alt+O，Ctrl+Alt+L

7.每个⽅法总⾏数不能超过80⾏

8.单⾏代码⻓度不能超过⼀屏幕(160字符)，若过⻓需及时换⾏

9.if语句必须添加⼤括号，即使逻辑只有⼀⾏代码，也需要，例如：

1 if（needRefresh）{

2 refresh();

3 }

10.⾮空判断，使⽤NullUtils.isNotNull(XX);

11.禁⽌使⽤strinng.equals(string)，字符串⽐较使⽤TextUtils.equals(string1,string2);

12.禁⽌直接使⽤TextView.setText();，TextView设置字符串使⽤TextViewUtils.setText(tv, str);

13.禁⽌在⾃定义View的onDraw⽅法⾥创建新对象

14.禁⽌在RecyclerViewHolder的onBindView中创建新对象

15.禁⽌在size超过10的for循环中创建新对象

16.弃⽤或不推荐⽅法，及时添加@Deprecated注解，如有新⽅法代替，请在注解中添加{@link XXX}

17.数据类型，不要直接使⽤int，须定义枚举

18.遇到需要使⽤HashMap的地⽅，使⽤ArrayMap代替

19.代码中遇到字符串拼接，禁⽌直接写死字符串，必须使⽤Resource.getString(R.string.str);

20.布局⽂件中，所有的宽⾼、字体⼤⼩必须引⽤@deimen

1 android:layout_width="@dimen/x100'

2 android:textSize="@dimen/x16"21.单⾏TextView，必须设置minHeight

22.多⾏TextView，必须设置⾏间距，引⽤@style/base_module_text_line_spacing_multiplier

23.提交代码中不能包含原⽣的Log打印，⽇志打印使⽤已封装的MyLog





















![1](https://ask.qcloudimg.com/http-save/yehe-1001569/100add2fc009e973308b771b5ddcda3e.png)
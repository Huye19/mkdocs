# MVP + 多模块方式

## 1.MVP模式的概要

MVP（Model-View-Presenter）是一种软件架构模式，用于将应用程序的逻辑和表示分离。它包含三个主要组件：模型（Model）、视图（View）和Presenter。

1. 模型（Model）：
   模型是应用程序的数据层，负责处理数据的获取、存储、操作和处理。它通常包含数据实体、数据库操作、网络请求等。模型不依赖于视图和Presenter，它只关注数据的处理和管理。
2. 视图（View）：
   视图是用户界面的展示层，负责显示数据和与用户进行交互。视图向用户展示数据，并将用户的操作传递给Presenter进行处理。视图应该尽量保持简单和无逻辑，它主要负责显示和响应用户的输入。
3. Presenter（Presenter）：
   Presenter充当了模型和视图之间的中间层，负责处理业务逻辑和协调模型和视图之间的交互。它接收用户输入和视图的回调，根据业务规则处理数据，并更新视图的状态。Presenter不直接操作数据，而是通过模型来处理数据操作。

## 2.MVP模式的工作流程

1. **用户操作触发事件：** 用户在View（通常是Activity或Fragment）上执行某种操作，例如点击按钮、输入文本等。
2. **View通知Presenter：** View将用户的操作通知给Presenter。通常，View中会有相应的回调接口或方法，Presenter会实现这些接口或调用这些方法，以便能够接收View的事件通知。
3. **Presenter处理业务逻辑：** Presenter接收到View的通知后，负责处理业务逻辑。这可能包括从Model中获取数据、对数据进行处理、更新数据等操作。
4. **Presenter更新Model：** 如果需要，Presenter可能会更新Model中的数据，例如进行网络请求、数据库操作等。
5. **Presenter更新View：** 一旦业务逻辑完成并且Model更新完毕，Presenter将更新的数据传递给View，以便更新用户界面。这通常通过调用View的方法或接口来实现。
6. **View更新UI：** View接收到Presenter传递的数据后，负责更新用户界面。这包括显示新的数据、刷新列表、更新图形元素等。

整个流程中，Model负责处理数据的获取、存储和处理，View负责显示数据和接收用户输入，而Presenter则是连接Model和View的中间层，负责应用程序的业务逻辑。

## 3.MVP模式的优点

- 分离关注点：将应用程序的逻辑与表示分离，提高了代码的可维护性和可测试性。
- 可扩展性：由于各个组件之间的松耦合关系，可以方便地对每个组件进行单独的修改和扩展。
- 可复用性：Presenter和模型可以在不同的视图中重复使用，提高了代码的重用性。
- 支持并行开发：开发人员可以同时进行模型、视图和Presenter的开发，提高开发效率。

## 4.MVP模式的示例

项目结构包括base接口(MVP的基础接口)、Baseactivity(抽象类)、契约接口Contract和MVP实现接口的类。

在MVP模式中，Base View接口可以定义一些通用的方法，用于与View层交互。这些方法可以包括：

1. 显示和隐藏加载进度条的方法：可以有`showLoading()`和`hideLoading()`方法，用于在View层显示和隐藏加载进度条，提供良好的用户体验。
2. 显示提示消息的方法：可以有`showMessage(String message)`方法，用于显示一条提示消息给用户，例如成功提示、错误提示等。
3. 显示和隐藏空数据视图的方法：可以有`showEmptyView()`和`hideEmptyView()`方法，用于显示和隐藏数据为空时的视图，例如空列表提示、空页面等。
4. 显示和隐藏错误视图的方法：可以有`showErrorView()`和`hideErrorView()`方法，用于显示和隐藏数据加载错误时的视图，例如网络错误提示、数据解析错误等。
5. 跳转到其他页面的方法：可以有`navigateTo(Class<?> destination)`方法，用于跳转到其他页面，可以通过参数传递目标页面的类。
6. 显示和隐藏键盘的方法：可以有`showKeyboard()`和`hideKeyboard()`方法，用于显示和隐藏软键盘。

Base Model是一个接口，用于定义Model层的通用方法。它可以包括以下内容：

1. 数据获取和处理的方法：包括从服务器获取数据、本地数据存储、数据加工处理等方法。
2. 数据回调和通知的方法：定义数据加载成功、失败等回调方法，以及通知Presenter层的方法。
3. 数据清理和释放资源的方法：包括清理缓存、关闭数据库连接、释放资源等方法。

Base Presenter是一个接口，用于定义Presenter层的通用方法。它可以包括以下内容：

1. 视图绑定和解绑的方法：定义绑定View和解绑View的方法，用于与具体的View进行交互。

2. 业务逻辑处理的方法：包括处理用户输入、响应View的事件、处理数据等方法。

3. 生命周期回调的方法：定义Presenter层的生命周期方法，例如onCreate、onStart、onResume等方法。

4. 错误处理和异常处理的方法：定义处理错误和异常情况的方法，例如网络错误、数据解析错误等。

   



BaseView：基础视图接口
BaseModel：基础模型接口
BasePresenter：基础Presenter接口
Contract：契约接口，可能定义了视图、模型和Presenter之间的交互合同
BaseActivity：基础Activity类
MainActivity：具体的Activity类
PresenterImpl：Presenter的实现类
ModelImpl：模型的实现类
这种结构是符合 MVP 模式的基本设计思想的，因为它将视图、模型和Presenter分离，并使用接口进行交互。这样的设计有助于解耦和测试，提高代码的可维护性和可扩展性。

BaseView、BaseModel和BasePresenter定义了通用的方法和行为，可以在具体的视图、模型和Presenter中进行扩展和实现。

Contract接口用于定义视图、模型和Presenter之间的契约，明确它们的职责和交互方式。通过契约接口，可以清晰地了解视图和Presenter之间的方法调用关系，提高代码的可读性和可维护性。

BaseActivity是一个基础的Activity类，可能提供一些通用的方法和行为，供具体的Activity类继承和使用。

MainActivity是具体的Activity类，它实现了视图接口，负责处理用户界面的展示和交互。

PresenterImpl是Presenter的具体实现类，它实现了Presenter接口，负责处理业务逻辑和协调视图和模型之间的交互。

ModelImpl是模型的具体实现类，它实现了模型接口，负责数据的获取和处理。





## 5.实战一个基于MVP模式的向后台请求登录的App：

### 一、准备：

在新建的项目中的模块名下面新建五个包，分别是Base、Presenter、View、Model、Contract。

Base中有三个泛型接口（该接口的泛型参数 `T` 必须是 `BasePresenter` 或其子类。）和一个类：BaseView、BaseActivity（实现了BaseView接口）、BaseModel、BasePresenter。

Contract包中创建IContract接口，再分别创建View、Presenter、Model三个接口。

Presenter中有一个实现Contract包中IContract接口的类：PresenterImpl

Model、View（继承BaseView）同理。

### 二、基础框架

#### 1.BaseModel：

```
public interface BaseModel<T extends BasePresenter> {
		//绑定p层
    void attachPresenter(T presenter);

}
```

接口 `BaseModel<T extends BasePresenter>` 定义了一个泛型接口 `BaseModel`，该接口的泛型参数 `T` 必须是 `BasePresenter` 或其子类。

接口中声明了一个方法 `attachPresenter(T presenter)`，用于将一个实现了 `BasePresenter` 接口的对象绑定到当前的模型（Model）中。通过该方法，Presenter 可以与对应的 Model 建立关联。

该方法的详细说明如下：

1. `void`：表示该方法没有返回值。
2. `attachPresenter`：方法名，用于绑定 Presenter。
3. `(T presenter)`：方法参数，表示需要传入一个类型为 `T` 的参数 `presenter`，这里的 `T` 是在接口声明时定义的泛型参数。
4. `T extends BasePresenter`：该方法的泛型参数约束，表示参数 `presenter` 的类型必须是 `BasePresenter` 或其子类。

通过实现该接口的类可以在方法中调用 `attachPresenter()` 方法，将对应的 Presenter 传递给 Model，并与其建立关联。这样，Presenter 和 Model 就可以进行交互，实现业务逻辑的处理。



#### 2.BaseView：

```
public interface BaseView {
		//提示消息
		void showMessage(String message);
		
}
```



#### 3.BasePresenter：

```
public interface BasePresenter<T extends BaseView, E extends BaseModel> {
    //绑定view
    用于将一个实现了 BaseView 接口的对象绑定到当前的 Presenter 中。通过该方法，Presenter 可以与对应的 View 建立关联。
    void attachView(T view);

    // 解绑
    void detachView();

    //绑定model
    public E attachModel();

    //解绑
    void detachModel();
}
```



#### 4.BaseActivity（抽象类）：

```
public abstract class BaseActivity<T extends BasePresenter> extends AppCompatActivity implements BaseView {
    protected T presenter;

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(getLayout());
    
        //创建presenter对象
        presenter = CreatePresenter();
        if (presenter != null) {
            presenter.attachView(this);
        }
    
        initial();
    }
    protected abstract int getLayout(); 
    
    protected abstract T CreatePresenter(); 
    
    protected abstract void initial();

}
```



#### 5.IContract：

```
public interface IContract {
    interface View extends BaseView {
       
    }
    
    interface Presenter extends BasePresenter<View,Model> {
        //p层接受v层的请求，向m层请求
        void handleLogin(String account, String password);
    
        //p层接受m层返回的信息,处理后向v层请求
        void resultLogin(Boolean result);
    
    }
    
    interface Model extends BaseModel<Presenter> {
        //处理登录
        void Login(String account, String password);
    }

}
```



#### 6.ModelImpl：

```
public class ModelImpl implements IContract.Model {
    
    private IContract.Presenter Presenter;
    
    @Override
    public void attachPresenter(IContract.Presenter presenter) {
        Presenter = presenter;
    }


    @Override
    public void Login(String account, String password) {

        OkHttpClient client = new OkHttpClient();
        String url = "http://192.168.31.178:8000/login/";
        JSONObject jsonObject = new JSONObject();
        try {
            jsonObject.put("account", account);
            jsonObject.put("password", password);
        } catch (JSONException e) {
            e.printStackTrace();
        }

        RequestBody requestBody =   RequestBody.create(MediaType.parse("application/json"), jsonObject.toString());

        Request request = new Request.Builder()
                .url(url)
                .post(requestBody)
                .build();

        client.newCall(request).enqueue(new Callback() {
            @Override
            public void onFailure(Call call, IOException e) {
            // 请求失败处理
            		e.printStackTrace();
                new Handler(Looper.getMainLooper()).post(new Runnable() {
                    @Override
                    public void run() {
                        Presenter.resultLogin(false);
                    }
                });

            }

            @Override
            public void onResponse(Call call, Response response) throws IOException {

            
                // 请求成功处理
                if (response.isSuccessful()) {

                    try{
                        ResponseBody responseBody = response.body();
                        if (responseBody != null) {
                            String responseData = responseBody.string();
                            JSONObject jsonObject1 = new JSONObject(responseData);

                            if ((jsonObject1.optString("message")).equals("登录成功")) {
                                new Handler(Looper.getMainLooper()).post(new Runnable() {
                                    @Override
                                    public void run() {
                                        Presenter.resultLogin(true);
                                    }
                                });
                            } else {
                                new Handler(Looper.getMainLooper()).post(new Runnable() {
                                    @Override
                                    public void run() {
                                        Presenter.resultLogin(false);
                                    }
                                });
                            }
                            responseBody.close();
                        }

                    }catch (Exception e){
                        e.printStackTrace();
                    }


                } else {


                    System.out.println("数据处理失败");
                    new Handler(Looper.getMainLooper()).post(new Runnable() {
                        @Override
                        public void run() {
                            Presenter.resultLogin(false);
                        }
                    });

                }
            }
        });

    }
}

```



#### 7.PresenterImpl：

```
public class PresenterImpl implements IContract.Presenter {
    private IContract.View View;
    private IContract.Model Model;

    @Override		//this.view 是在当前类中使用的引用，用于明确指示当前类中的成员变量 view
    public void attachView(IContract.View view) {
        this.View = view;
        this.Model =attachModel();
        this.Model.attachPresenter(this);
    }

    @Override
    public void detachView() { this.View = null; }

    @Override
    public ModelImpl attachModel() {
        return new ModelImpl(); 
    }

    @Override
    public void detachModel() { Model = null; }


    @Override
    public void handleLogin(String account, String password) {
        Model.Login(account, password);
    }

    @Override
    public void resultLogin(Boolean result) {
        if (result) {
            View.loginResult("登录成功");
        } else {
            View.loginResult("登录失败");
        }
    }
}
```



#### 8.MainActivity：

```
public class MainActivity extends BaseActivity<PresenterImpl> implements IContract.View {

    EditText account;
    EditText password;
    Button button;


    @Override
    protected int getLayout() {
        return R.layout.activity_main;
    }

    @Override
    protected PresenterImpl CreatePresenter() {
        return new PresenterImpl();
    }

    @Override
    protected void initial() {
        account = findViewById(R.id.et_account);
        password = findViewById(R.id.et_password);
        button = findViewById(R.id.button);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                presenter.handleLogin(account.getText().toString(), password.getText().toString());
            }
        });
    }

    @Override
    public void loginResult(String Msg) {
        Toast.makeText(this,Msg, Toast.LENGTH_SHORT).show();
    }
}
```

登录功能已实现，响应慢，待解决。



## 6.MVP的绑定

### 一、

​		MVP模式中的绑定是通过Presenter构造函数来实现的，View在创建Presenter实例时传递自身给Presenter，从而建立了双向关联。解绑是通过在Activity（或Fragment）的生命周期方法（例如onDestroy）中调用Presenter的解绑方法来实现的。这样可以确保在Activity销毁时解除View和Presenter之间的关联，避免内存泄漏。



### 二、实现绑定关键代码：

##### 1.PresenterImpl.java中：

```
private IContract.IView View;
private IContract.IModel Model;
@Override
public void attachView(IContract.IView view) {
    View = view;
    Model = attachModel();//实现绑定m层
    Model.attachPresenter(this);//调用m层方法时将自身传递过去实现m层绑定p层
}
@Override
public IContract.IModel attachModel() {
    return new ModelImpl();
}
```



##### 2.ModelImpl.java中：

```
private IContract.IPresenter Presenter;

@Override
public void attachPresenter(IContract.IPresenter presenter) {
    Presenter = presenter;//p层调用此方法时将自身传递过来实现绑定p层
}
```



##### 3.BaseActivity.java中：

```
public abstract class BaseActivity<T extends BasePresenter> extends AppCompatActivity implements BaseView 


protected T Presenter;

Presenter = CreatePresenter();//实现绑定p层
if (Presenter != null) {
    Presenter.attachView(this);//调用p层方法时将自身传递过去实现p层绑定v层
}

protected abstract T CreatePresenter();
```



##### 4.MainActivity.java中：

```
public class MainActivity extends BaseActivity<PresenterImpl> implements IContract.IView

@Override
protected PresenterImpl CreatePresenter() {
    return new PresenterImpl();
}
```



## 7.OkHttp的使用：

```
public class ModelImpl implements IContract.IModel {

    private static final String TAG = "modelImpl";

    private IContract.IPresenter Presenter;
    @Override
    public void attachPresenter(IContract.IPresenter presenter) {
        Presenter = presenter;
    }

    @Override
    public void Login(String account, String password) {

        OkHttpClient client = new OkHttpClient();
        //创建OkHttpClient实例，用于发送HTTP请求：
        String url = "http://192.168.31.178:8000/login/";
        //提前将url存储在变量中
        JSONObject jsonObject = new JSONObject();
        //用于存储json格式的数据
        try {
            jsonObject.put("account", account);
            jsonObject.put("password", password);
        } catch (JSONException e) {
            e.printStackTrace();
        }
        //将键值对写入jsonObject
        RequestBody requestBody = RequestBody.create(MediaType.parse("application/json"),jsonObject.toString());
        //使用RequestBody.create方法从jsonObject中创建请求体。第一个参数是指定请求体的类型，这里是json格式，第二个参数是请求体的内容
        //toString将JSONObject对象中的键值对转换为JSON格式的字符串
        Request request = new Request.Builder()
                .url(url)
                .post(requestBody)
                .build();
        //构建一个HTTP请求，创建了一个Request.Builder对象，用于设置请求的各种属性。
        //.build()：这是用于构建最终的Request对象的方法。在设置完所有请求属性后，我们调用.build()方法来创建Request对象。
        
        
        
        
        
        

				通过enqueue方法，异步发送HTTP请求，Callback对象用于处理请求结果。
        client.newCall(request).enqueue(new Callback() {
            @Override
            public void onFailure(Call call, IOException e) {
            // 请求失败处理
            		e.printStackTrace();
                new Handler(Looper.getMainLooper()).post(new Runnable() {
                    @Override
                    public void run() {
                        Presenter.resultLogin(false);
                    }
                });

            }


						如果请求成功，在onResponse方法中，首先获取响应数据并解析为JSON对象。如果JSON对象中的"message"字段值为"登录成功"，则通过Handler切换到主线程，调用Presenter的resultLogin(true)方法通知结果为true；否则，调用resultLogin(false)方法通知结果为false。
            @Override
            public void onResponse(Call call, Response response) throws IOException {

            
                // 请求成功处理，判断响应码
                if (response.isSuccessful()) {

                    try{
                        ResponseBody responseBody = response.body();
                        if (responseBody != null) {
                            String responseData = responseBody.string();//拿到返回所有内容
                            JSONObject jsonObject1 = new JSONObject(responseData);
														解析为JSON对象，通过optString方法拿到值
                            if ((jsonObject1.optString("message")).equals("登录成功")) {
                                new Handler(Looper.getMainLooper()).post(new Runnable() {
                                    @Override
                                    public void run() {
                                    更新UI必须在主线程，通过Handler实现
                                        Presenter.resultLogin(true);
                                    }
                                });
                            } else {
                                new Handler(Looper.getMainLooper()).post(new Runnable() {
                                    @Override
                                    public void run() {
                                        Presenter.resultLogin(false);
                                    }
                                });
                            }
                            responseBody.close();
                        }

                    }catch (Exception e){
                        e.printStackTrace();
                    }


                } else {


                    System.out.println("数据处理失败");
                    new Handler(Looper.getMainLooper()).post(new Runnable() {
                        @Override
                        public void run() {
                            Presenter.resultLogin(false);
                        }
                    });

                }
            }
        });

    }
    
    !response.isSuccessful() 是在 onResponse 方法中对请求结果的HTTP状态码进行判断，用于判断请求是否失败。
public void onFailure(Call call, IOException e) 是通过实现 Callback 接口的 onFailure 方法来处理请求失败的逻辑，当请求失败时，OkHttp将调用该方法并传递失败的信息。
```






















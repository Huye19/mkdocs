# Android多模块开发实例：



### 1.建立项目与多个模块：

#### config.gradle

建立公共环境文件config.gradle，添加isRelease = true，以此来决定各个module是一体还独立。

```
ext {
    isRelease = true

    dependencies = [
            //原始依赖
            "appcompat"       : 'androidx.appcompat:appcompat:1.6.1',                 //implementation
            "material"        : 'com.google.android.material:material:1.11.0',        //implementation
            "constraintlayout": 'androidx.constraintlayout:constraintlayout:2.1.4',   //implementation
            "junit"           : 'junit:junit:4.13.2',                                 //testImplementation
            "ext:junit"       : 'androidx.test.ext:junit:1.1.5',                      //androidTestImplementation
            "espresso"        : 'androidx.test.espresso:espresso-core:3.5.1',          //androidTestImplementation


            //组件
            "sweetalert"      : 'com.github.f0ris.sweetalert:library:1.5.1', //提示框


            //功能框架
            "arouter"         : 'com.alibaba:arouter-api:1.5.1',            //阿里ARouter路由

            
    ]
}
```



#### 创建基础模块和功能模块

将基础模块创建为Android Library，功能模块创建为Phone & Tablet Module。区别在于一个有资源文件，一个没有。

假设已经创建了component_base和module_login模块



#### build.gradle

在根配置文件（build.gradle）中引入，在根配置文件中配置后，其他模块才能调用config.gradle里面的参数

```
apply from: 'config.gradle'
```

在主模块中引入功能模块：

```
if (isRelease) {
    implementation project(':module_login')
}
```



#### gradle.properties

在项目的 `gradle.properties` 文件中添加以下行：

解决旧版的 Support 库与新版 AndroidX 库之间的依赖冲突。

```
android.enableJetifier=true
```



#### settings.gradle

添加镜像源：

```
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        maven { url 'https://jitpack.io' }
        maven { url 'https://maven.aliyun.com/repository/google' }
        maven { url 'https://maven.aliyun.com/repository/jcenter' }
        maven { url 'https://maven.aliyun.com/repository/gradle-plugin' }
        google()
        mavenCentral()
    }
}
```



#### app模块

app模块下的build.gradle文件修改

```
dependencies {

    implementation 'androidx.appcompat:appcompat:1.6.1'
    implementation 'com.google.android.material:material:1.11.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.4'
    testImplementation 'junit:junit:4.13.2'
    androidTestImplementation 'androidx.test.ext:junit:1.1.5'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.5.1'


    if (isRelease) {
        implementation project(':module_login')
    } else {
        implementation project(':component_base')
    }
}
```



AndroidManifest.xml文件修改

```
<application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.MvpDemo"
        tools:targetApi="31">
        <activity
            android:name="com.smartlab411.module_login.MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
```







#### app.gradle

因为我们的app主模块、app-setting和app-video模块的build.gradle，里面很多配置都差不多，所以我们可以新建一个app.gradle文件，用来统一配置，如下：为app.gradle里面的内容

```
if (isRelease) {
    plugins.apply('com.android.library')
} else {
    plugins.apply('com.android.application')
}
android {
    compileSdk 33

    defaultConfig {
        minSdk 24
        targetSdk 33

        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
        //用到RAouter时添加
        javaCompileOptions {
            annotationProcessorOptions {
                arguments = [AROUTER_MODULE_NAME: project.getName()]
            }
        }
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}
dependencies {
		//一般依赖直接在base模块导入，但注解依赖是个例外
    annotationProcessor rootProject.ext.dependencies["arouter-compiler"]
		
    //在通用的app.gradle模块中引入基模块，这样其它模块就可以调用module_base中的资源
    implementation project(':module_base')
}
```

这样module_login模块就能够在其gradel文件引入app.gradel

```
apply from: '../app.gradle'

android {
    namespace 'com.smartlab.module_login'

    defaultConfig {

        //如果是发布版，改模块为library，是不能设置applicationId的
        if (!isRelease) {
            applicationId "com.smartlab.module_login"
            versionCode 1
            versionName "1.0"
        }

    }


}

dependencies {


}
```



component_base



#### 后续添加模块则修改模块中build.gradle文件同上


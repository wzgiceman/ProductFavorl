# ProductFavorl
变种多渠道打包demo

##运行场景
同一款软件，因为定制和其他原因，需要打包多个版本，每个版本都有各自的特色和区别（整体显示大致一样），而且能同时安装到一个手机（具有不同的包名）

##运行技术
AndroidStudio 打包中的productFlavors

##使用方法
```java
android {
    compileSdkVersion 23
    buildToolsVersion "23.0.2"
    defaultConfig {
        applicationId "com.wzgiceman.productfavorl"
        minSdkVersion 17
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
    }

    productFlavors {
        fulls {
            applicationId "com.wzgiceman.productfavorl.fulls"
            versionName "1.0-fulls"
        }
        demo {
            applicationId "com.wzgiceman.productfavorl.demo"
            versionName "1.0-demo"
        }
    }

}
```
defaultConfig定义的是默认的属性，productFlavors的是每一个单独的属性，productFlavors会覆盖defaultConfig属性，所以上面的写法可以理解成：

```java
 productFlavors {
        fulls {
            applicationId "com.wzgiceman.productfavorl.fulls"
            versionName "1.0-fulls"
            minSdkVersion 17
            targetSdkVersion 23
            versionCode 1
        }
        demo {
            applicationId "com.wzgiceman.productfavorl.demo"
            versionName "1.0-demo"
            minSdkVersion 17
            targetSdkVersion 23
            versionCode 1
        }
    }
```

这样AS默认就会构建两个项目，其中一个是fulls，一个是demo，他们公用一个项目main（com.wzgiceman.productfavorl）；但是可惜的是AS并不会自动
生成这两个的工程文件，需要手动创建如下：





* 传统对比
```java
android {
    compileSdkVersion 23
    buildToolsVersion "23.0.2"
    defaultConfig {
        applicationId "com.wzgiceman.productfavorl"
        minSdkVersion 17
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
    }
```

##实现效果
1. demo渠道-包名：com.wzgiceman.productfavorl.demo
![](https://github.com/wzgiceman/ProductFavorl/blob/master/gif/demo.gif)
2. full渠道-包名：com.wzgiceman.productfavorl.fulls
![](https://github.com/wzgiceman/ProductFavorl/blob/master/gif/full.gif)

##实现方法


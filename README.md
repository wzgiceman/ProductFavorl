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

##效果
1. demo渠道-包名：com.wzgiceman.productfavorl.demo

![](https://github.com/wzgiceman/ProductFavorl/blob/master/gif/demo.gif)

2. full渠道-包名：com.wzgiceman.productfavorl.fulls

![](https://github.com/wzgiceman/ProductFavorl/blob/master/gif/full.gif)

##实现方法

**我们分别在demo和fulls中创建一个SecendActivity**
**构建完成后的工程目录**

![](https://github.com/wzgiceman/ProductFavorl/blob/master/gif/a1345078-1dd5-4876-8cc8-d64fc250bc1f.png)

分别创建对应的xml-layout，区分不同：

**demo-layout**

```java
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
    android:id="@+id/activity_secend"
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    >


    <TextView android:layout_width="wrap_content"
              android:textColor="@color/colorAccent"
              android:text="@string/text"
              android:layout_height="wrap_content"/>

</RelativeLayout>

```
**fulls-layout**

```java
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
    android:id="@+id/activity_secend"
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    >


    <TextView android:layout_width="wrap_content"
              android:text="@string/text"
              android:textColor="@color/colorPrimary"
              android:textSize="33sp"
              android:layout_height="wrap_content"/>

</RelativeLayout>
```

**通过build variant选择当前要构建的工程**

可以明显的看出demo是工程build模式，但是fulls没有build；这个需要开发者自己去切换

![](https://github.com/wzgiceman/ProductFavorl/blob/master/gif/9dbdb097-6a93-43da-b686-23b2b36b1731.png)

**注意： 当你修改了项目中的构建文件， Android Studio 需要一个项目同步来导入构建配置的改变。点击出现在 Android Studio 黄色通知栏上的 Sync Now 按钮来导入这些变化**

**配置 AndroidManifest**

```java
  <activity android:name=".SecendActivity"> </activity>
```
##运行

测试模式下需要选择对应的debug模式运行







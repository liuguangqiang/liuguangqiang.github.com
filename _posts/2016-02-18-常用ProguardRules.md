---
layout : post 
category : Android
tags : [Android]
desc : Android中常用的Proguard Rules，备忘一下，妈妈再也不用担心我的代码混淆了...

title : 常用Proguard Rules
---

Android中常用的Proguard Rules，备忘一下，妈妈再也不用担心我的代码混淆了...

## Annotation

```java
-keepattributes *Annotation*
-keep class javax.inject.** { *; }
```

## EventBus

```java
-keep class de.greenrobot.** { *; }
-keepclassmembers class ** {
    public void onEvent*(**);
}
```

## Dagger2.0

```java
-keep class dagger.** { *; }
-keep interface dagger.** { *; }

-keep class **$$ModuleAdapter { *; }
-keepnames class **$$InjectAdapter { *; }
-keepclassmembers class * {
    @javax.inject.Inject <fields>;
    @javax.inject.Inject <init>(...);
}
-adaptclassstrings
```

## Glide

```java
-keep public class * implements com.bumptech.glide.module.GlideModule
-keep public enum com.bumptech.glide.load.resource.bitmap.ImageHeaderParser$** {
    **[] $VALUES;
    public *;
}
```

## Gson

```java
-keepattributes Signature
-keep class sun.misc.Unsafe { *; }
-keep class com.google.gson.examples.android.model.** { *; }
```

## LoganSquare

```java
-keep class com.bluelinelabs.logansquare.** { *; }
-keep @com.bluelinelabs.logansquare.annotation.JsonObject class *
-keep class **$$JsonObjectMapper { *; }
```

## ButterKnife

```java
-keep class butterknife.** { *; }
-dontwarn butterknife.internal.**
-keep class **$$ViewBinder { *; }

-keepclasseswithmembernames class * {
    @butterknife.* <fields>;
}

-keepclasseswithmembernames class * {
    @butterknife.* <methods>;
}
```

## RxJava & RxAndroid

最麻烦的就是RxJava和RxAndroid，直到我遇到下面的library

```
compile 'com.artemzin.rxjava:proguard-rules:1.1.0.0'
```

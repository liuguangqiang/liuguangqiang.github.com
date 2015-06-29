---
layout : post 
category : Android
tags : [Android]
desc : LeakCanary介绍

title : LeakCanary介绍
---

## LeakCanary是什么鬼？
LeakCanary又是一个出自square的良心之作！
专为Android和Java检测内存泄漏而生。

	“A small leak will sink a great ship.” - Benjamin Franklin
 
![image](/content/leakcanary.png)

## 开始使用
在build.gradle中添加依赖

```
 dependencies {
   debugCompile 'com.squareup.leakcanary:leakcanary-android:1.3.1'
   releaseCompile 'com.squareup.leakcanary:leakcanary-android-no-op:1.3.1'
 }
```

在Application中初始化

{% highlight java %}
public class ExampleApplication extends Application {

  @Override public void onCreate() {
    super.onCreate();
    LeakCanary.install(this);
  }
  
}
{% endhighlight %}

## 为什么要使用LeakCanary?

## 如何使用
用Refwatcher监控应该要回收的引用

{% highlight java %}
RefWatcher refWatcher = {...};

// We expect schrodingerCat to be gone soon (or not), let's watch it.
refWatcher.watch(schrodingerCat);
{% endhighlight %}

LeakCanary.install() 会返回一个预先配置好的 RefWatcher。同时也会安装一个ActivityRefWatcher, 它会自动监控一个Activity调用onDestory()后的内存泄漏。

{% highlight java %}
public class ExampleApplication extends Application {

  public static RefWatcher getRefWatcher(Context context) {
    ExampleApplication application = (ExampleApplication) context.getApplicationContext();
    return application.refWatcher;
  }

  private RefWatcher refWatcher;

  @Override public void onCreate() {
    super.onCreate();
    refWatcher = LeakCanary.install(this);
  }
}
{% endhighlight %}

也可以用RefWatcher来监控fragment的内存泄漏
{% highlight java %}
public abstract class BaseFragment extends Fragment {

  @Override public void onDestroy() {
    super.onDestroy();
    RefWatcher refWatcher = ExampleApplication.getRefWatcher(getActivity());
    refWatcher.watch(this);
  }
}
{% endhighlight %}

## LeakCanary是如何工作的？
1. RefWatcher.watch() 会创建一个 KeyedWeakReference 到被监控对象。
2. 然后, 在后台线程中检查对象的引用是否被清除，如果没有, 则调用GC。
3. 如果最终还是没有被清除, 就把heap到.hprof文件中，并存到文件系统中。

## 未完待续！
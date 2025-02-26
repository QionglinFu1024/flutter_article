appbar版本-动画关闭

单、多引擎嵌套

初始化引擎组，开一个空的flutter路由引擎，



dart单线程isolate flutter多线程GPU、UI、IO、platform

​	https://juejin.cn/post/6844903831478730759

var、dynamic、object有什么区别

国际化语言

[TOC]



## flutter生命周期

Flutter 生命周期指的是应用程序中每个界面或页面的生命周期。具体来说，就是当页面从创建、渲染、暂停、恢复、销毁等一系列状态变化的过程。在 Flutter 中，`StatefulWidget` 和 `StatelessWidget` 是两种常见的组件类型，它们的生命周期有所不同。

### 1. `StatelessWidget` 生命周期

`StatelessWidget` 是没有状态的组件，它的生命周期比较简单，通常只会经历以下几个阶段：

- **`build()`**：构建 UI。每次组件需要重新构建时都会调用这个方法。

### 2. `StatefulWidget` 生命周期

`StatefulWidget` 是有状态的组件，生命周期更加复杂。主要涉及以下几个方法：

- **`createState()`**：每次创建 `StatefulWidget` 时调用。返回一个与 `StatefulWidget` 关联的 `State` 对象。
- **`initState()`**：在 `State` 对象被创建后、组件的状态首次插入树之前调用。用于做一些初始化操作，比如异步请求、初始化动画等。这个方法只会调用一次。
- **`didChangeDependencies()`**：当 `State` 对象的依赖发生变化时调用。例如，`InheritedWidget` 发生变化时，会调用这个方法。这个方法在 `initState()` 之后调用，但也会在 `State` 的生命周期中多次调用。
- **`build()`**：每次当 `State` 需要重新构建时都会调用。无论是因为父组件重建，还是因为组件内部的状态发生变化，都会调用这个方法。
- **`didUpdateWidget()`**：当父组件重建并传递新的 `StatefulWidget` 时调用。如果 `State` 还没有被销毁，那么会调用此方法。
- **`setState()`**：调用这个方法会触发 `build()` 方法的重建。可以在这里更新状态，重新构建界面。
- **`deactivate()`**：当 `State` 对象从树中移除时调用。它被调用时，组件并没有完全销毁，可能会被重新插入树中。
- **`dispose()`**：当 `State` 对象即将被销毁时调用。可以在这里清理资源，比如取消定时器、关闭流、释放动画控制器等。

### 3. 页面生命周期方法

对于整个页面的生命周期，通常我们会使用 `WidgetsBindingObserver` 来监听以下事件：

- **`didChangeAppLifecycleState()`**：当应用的生命周期发生变化时调用（如切换到后台、恢复到前台）。例如，你可以在这里处理暂停/恢复时的逻辑。

  ```
  dart
  
  
  复制编辑
  WidgetsBinding.instance.addObserver(MyObserver());
  
  class MyObserver extends WidgetsBindingObserver {
    @override
    void didChangeAppLifecycleState(AppLifecycleState state) {
      if (state == AppLifecycleState.paused) {
        // 应用进入后台
      } else if (state == AppLifecycleState.resumed) {
        // 应用恢复到前台
      }
    }
  }
  ```

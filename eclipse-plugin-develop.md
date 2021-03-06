eclipse 插件开发
===

## 插件开发环境

eclipse 提供了插件开发环境 (PDE),
可以直接下载包含了 PDE 的 all-in-one 包, 如 jee 包,
或者从 eclipse 自带的 "update site" 安装.
从 "update site" 安装还可以同时安装插件源码和开发插件的相关文档.

[[eclipse-plugin-develop/install-pde.png]]

eclipse 自带的插件通常包含两个包,
一个是插件本身, 一个是开发者包.
开发者包包含插件源码和在插件上开发插件的文档, 包含插件扩展点详细文档.
安装了插件的源码包后,
依赖插件开发时 eclipse 就会自动定位到插件的源码, 非常方便.
插件 jar 包提供了 plugin.xml 文件, 
配合源码包可以很方便的学习插件开发代码.

"Eclipse Platform" 是运行时内核,
"Eclipse Platform SDK" 包含了运行时内核的插件开发文档和扩展点文档.
安装这个包就可以在 eclipse 的帮助文档中看到 "Platform Plug-in Developer Guide".
也可以直接从网上 [eclipse help](http://help.eclipse.org/kepler/index.jsp) 查看 eclipse 所有文档,
但安装在本地查看会更流畅.
注意 "Eclipse Platform SDK" 和 "Eclipse SDK" 不一样.

[[eclipse-plugin-develop/help-plugin-develop.png]]

开发 java 插件经常可以复用 JDT 插件的很多功能,
安装 JDT 的开发者包后,
开发时就可以非常方便的查看这些类的源码.

[[eclipse-plugin-develop/install-jdt.png]]

## plugin.xml 编辑设置

"plugin.xml" 文件默认是以 3 个空格作为缩进,
自动补全代码时自动生成的代码也是以这样的格式排版.
但 eclispe 没有提供对这个文件自动格式化的功能 (或者我没有找到),
按 "Ctrl + Shift + F" 没有任何效果,
所以最好编辑时就把格式写对.
eclipse 默认是以 Tab 缩进, 
编辑时使用 Tab 键就会导致 Tab 和空格混排, 格式不规范.
因此可以设置编辑 "plugin.xml" 时将 Tab 替换为 3 个空格.
"plugin.xml" 编辑器设置没有这个单独的设置,
只能修改全局编辑器的设置,
需要注意对编辑其他文件有没有影响.

[[eclipse-plugin-develop/plugin-xml-edit.png]]

## 学习其他插件

开发 eclipse 插件最好的办法就是 "山寨",
找一个功能类似的插件, 看看别人是怎么实现的, 然后依葫芦画瓢.

## 三方库

[eclipse orbit](http://eclipse.org/orbit/) 
项目提供了一些可以在 eclipse 中使用的 3 方库的 bundle,
如 logback.classic 二进制包和源码.
从 orbit 下载页面, 
如 [R20130827064939](http://download.eclipse.org/tools/orbit/downloads/drops/R20130827064939/),
可以找到 update site 链接
http://download.eclipse.org/tools/orbit/downloads/drops/R20130827064939/repository/
,
或者直接从页面链接下载.

## 

eclipse 运行环境和其他插件提供的很多功能, 服务和常量等, 
直接使用类的静态方法, 静态成员暴露出来, 非常方便调用.
如:

```java
IWorkbench org.eclipse.ui.PlatformUI.getWorkbench()
void org.eclipse.debug.ui.DebugUITools.launch(ILaunchConfiguration configuration, String mode)
org.eclipse.jdt.launching.IJavaLaunchConfigurationConstants.ATTR_PROJECT_NAME
org.eclipse.debug.ui.IDebugUIConstants.ATTR_LAUNCH_IN_BACKGROUND
```

还有一些服务是需要实例调用的, 
但是可以通过静态方法拿到对象实例.
如:

```java
ILaunchManager launchManager = DebugPlugin.getDefault().getLaunchManager();

```



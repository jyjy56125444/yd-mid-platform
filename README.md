# Android工作平台开发指南

[^作者]: 产品事业部 王一凡

[版本]: v2.0

 ***写在前面：***

*本文档根据《远大Android工作平台2.0》编写，目标是定义基础的设计开发理念，标准统一进而降低故障率和维护成本。*

*文档主要分为 Android文件命名与编写规范，基类与工具类api的说明，框架基本组件的定义与使用三大部分。提倡开发者遵循手册约定的编码规范和开发方式，熟练运用框架提供的api，避免重复申明对象、方法造成代码或逻辑冗余。*



# 第一章   开发规范

## 1.1  编码规范

### 1.1.1规范制定原则

- 方便代码的交流和维护。

- 不影响编码的效率，不与大众习惯冲突。

- 使代码更美观、阅读更方便。

- 使代码的逻辑更清晰、更易于理解。

### 1.1.2 IDE设置和快速格式化方式

`AndroidStudio`中设置代码格式化规范和注释规范，具体参考开发环境配置章节

代码格式化快捷键：`ctrl+shift+f`

代码注释快捷键：`ctrl+shift+/` 或者` ctrl+/`

### 1.1.3代码外观

类属性和类方法不要交叉放置，不同存取范围的属性或者方法也尽量不要交叉放置。格式：类定义

```
{ 
 类的公有属性定义
 类的保护属性定义
 类的私有属性定义
 类的公有方法定义
 类的保护方法定义
 类的私有方法定义
}
```

### 1.1.4列宽

代码列宽控制在110字符左右。以不出现横向滚动条为基准。

### 1.1.5换行

当表达式超出或即将超出规定的列宽，遵循以下规则进行换行：

- 在逗号后换行。

- 在操作符前换行。

- 规则1优先于规则2。

当以上规则会导致代码混乱的时候自己采取更灵活的换行规则。

### 1.1.6缩进

缩进应该是每行一个Tab(4个空格)，不要在代码中使用Tab字符。

### 1.1.7空行

空行是为了将逻辑上相关联的代码分块，以便提高代码的可阅读性。

在以下情况下使用两个空行：

- 接口和类的定义之间。

- 枚举和类的定义之间。

- 类与类的定义之间。    

在以下情况下使用一个空行：

- 方法与方法、属性与属性之间。
- 方法中变量声明与语句之间。
- 方法与方法之间。
- 方法中不同的逻辑块之间。
- 方法中的返回语句与其他的语句之间。
- 属性与方法、属性与字段、方法与字段之间。
- 注释与它注释的语句间不空行，但与其他的语句间空一行。如：

```
/**
  * 方法1
  */
public abstract void inData() throws IOException {}
    
/**
  * 方法2
  */
public abstract void outData() throws IOException {}
```

### 1.1.8空格

在以下情况中要使用到空格

- 关键字和左括符 “(” 应该用空格隔开。如：​   

```  try{
while (true){

}catch (Exception e){

}
```

- 多个参数用逗号隔开，每个逗号后都应加一个空格。

- 除此之外，所有的二元操作符都应用空格与它们的操作数隔开，一元操作符、++及--与操作数间不需要空格。如：

```
while (d++ = s++) {
	n++;
}

PrintSize(“size is “ + size + “\n”);

text.setText(a==true ? "正确" : "错误");
```

<font color="grey">**注：**在方法名和左括符 “(” 之间不要使用空格，这样有助于辨认代码中的方法调用与关键字。 </font>

### 1.1.9括号 - ()

- 左括号“(” 不要紧靠关键字，中间用一个空格隔开。

- 左括号“(” 与方法名之间不要添加任何空格。

- 没有必要的话不要在返回语句中使用()。如：

  ```return (1)```

### 1.1.10花括号 - {}

- 左花括号 “{” 放于关键字或方法名的同一行尾。如：

```
if (condition) {

}

public int add(int x, int y) {

}
```

- 左花括号 “{” 要与相应的右花括号 “}”对齐。

- 通常情况下左花括号 “{”接在行尾”}”单独成行，不与任何语句并列一行。

- if、while、do语句后一定要使用{}，即使{}号中为空或只有一条语句。如：

```
if (somevalue == 1) {
	somevalue = 2;
}
```

- 若折叠层次过多,右花括号 “}” 后建议加一个注释以便于方便的找到与之相应的 {。如：

```
while (1) {

if (valid) {

} // if valid
else{

} // not valid

} // end forever
```

## 1.2  命名规范

文件命名规范最终目的是为了让项目结构更加清晰易懂方便查找。

### 1.2.1约定空格

逗号隔开，每个逗号后都应 包名、文件夹名、类名、方法名都是以英文名为主，尽量按照驼峰式规则。

### 1.2.2约定

框架分为两个部分：核心类库层、业务层。

- 核心类库主要目录为`frame`，其中包含`action、acty、frags`等，还有一些第三方库。 

- 每个业务逻辑目录分为`action、actys、adapter、frgs、model、task、utils、db、views`等，分别对应业务逻辑处理、activity页面、数据适配器、fragment页面、对象模型、数据请求、工具、数据库、自定义控件。

### 1.2.3项目命名规范


- 框架包名为`com.sinoyd`，新项目**不允许**修改包名。
  新建项目后**必须**修改项目`Application ID`：

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/ApplicationId.png)


- 个性化开发功能模块时要在`com.sinoyd`目录下创建以项目名缩写命名的目录。
  下图为Showcase项目结构：

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/appTree.png)

### 1.2.4文件命名规范

文件命名按照驼峰式标准，统一以所在业务模块名缩写开头，以当前目录名结尾。使用项目名称_功能名称的方式 示例：

功能模块下actys目录：

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/actys.png)

adapter目录：

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/adapter.png)

### 1.2.5资源文件命名规范

- layout文件的命名方式，所有文件需以项目名称缩写作为开头，结尾方式如下： 

```
Activity的layout以_activity结尾
Fragment的layout以_fragment结尾
Dialog的layout 以_dialog结尾 
include的layout以_include结尾
ListView的行layout 以_list_item结尾 
RecyclerView的item layout 以_recycle_item结尾
GridView的item layout 以_grid_item结尾
```

​	文件命名示例：

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/res.png)

- Id资源原则上以驼峰法命名，View组件的资源id 建议以View的缩写作为 前缀。常用缩写表如下： 

| 控件               | <div style="width: 150pt">缩写</div> |
| ------------------ | ------------------------------------ |
| `LinearLayout`     | ll                                   |
| `RelativeLayout`   | rl                                   |
| `ConstraintLayout` | cl                                   |
| `ListView`         | lv                                   |
| `ScollView`        | sv                                   |
| `TextView`         | tv                                   |
| `Button`           | btn                                  |
| `ImageView`        | iv                                   |
| `CheckBox`         | cb                                   |
| `RadioButton `     | rb                                   |
| `EditText `        | et                                   |

- 图片根据其分辨率，放在不同屏幕密度的drawable目录下管理，否则可能在低密度设备上导致内存占用增加，又可能在高密度设备上导致图片显示不够清晰（此项不作为强制要求）。


### 1.2.6文件注释规范

1）对于新建的类，如`Activity，Fragment，Adapter`等，需要在头部添加注释信息，包括作者、创建时间、版权、描述等。

头部注释示例：

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/header2.png)

附`AndroidStudio`中添加文件头部注释方法：

打开`File ->Settings ->File and Code Templates ->includes -> File Header`

```
/**
  * 作者： 作者姓名
  * 创建时间： ${DATE}
  * 更新时间： ${DATE}
  * 描述： ${PACKAGE_NAME}
  * 版权： 江苏远大信息股份有限公司
 */
```

2）对于项目中使用的一些重要方法和变量，需要对其进行注释。方法注释使用 `/**`标注参数及返回值说明，方法中业务逻辑及变量注释采用双斜杠`//`

- 变量注释示例：

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/vail.png)

- 方法注释示例：

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/method.png)

<font color="grey">**注**：原则上，在项目开发过程中，所有变量及方法都需要进行注释。但是考虑到实际开发进度要求及工作量的庞大，建议在重要及复用性较高的方法上添加备注，同时，变量名称应尽可能表达**业务含义**，比如车辆信息命名为：carName，简单明了。</font>



# 第二章   框架使用

## 2.1  框架目录简介

`frame`文件夹包含所有工具类，超类以及部分组件。以下是各文件夹介绍：

| 文件夹        | 备注                       |
| ------------- | -------------------------- |
| `action`      | 框架逻辑处理               |
| `actys`       | 框架UI及UI基类（Activity） |
| `adapter`     | 通用适配器                 |
| `annotation`  | 注解注册及解释器           |
| `application` | 应用全局配置项             |
| `config`      | 框架参数及项目参数配置     |
| `db`          | 数据库相关                 |
| `frgs`        | 框架UI（Fragment）         |
| `model`       | 数据对象模型               |
| `task`        | 异步任务、网络请求         |
| `util`        | 通用工具类                 |
| `views`       | 框架视图库                 |
| `other`       | 保留                       |


## 2.2  全局`FrmApplication`配置

android系统会为每个程序运行时创建一个Application类的对象且仅创建一个，所以Application可以说是单例 (singleton)模式的一个类。且application对象的生命周期是整个程序中最长的，它的生命周期就等于这个程序的生命周期。因为它是全局的单例的，所以在不同的Activity，Service中获得的对象都是同一个对象。所以通过Application可以进行一些数据传递，数据共享，数据缓存等操作。

目前框架使用的`FrmApplication`继承自`BaseApplication`，其中有以下初始化操作：

1）文件夹目录创建

```
FileConfig.initFolders();
```

2）配置系统异常捕获机制

```
Thread.setDefaultUncaughtExceptionHandler(handler);
```

3）初始化权限全局监听

```
PermissionUtil.init(this)
```


## 2.3  框架参数配置

### 2.3.1网络通信基本设置


在`com.sinoyd.frame.config.AppBaseConfig`文件中

1）设置app网络通信地址

```
private static String defaultUrl = "https://om.envchina.com/api";//接口初始地址（个性化配置 *必须修改）
```

2）设置app图片网络地址（前缀可选）

```
private static String defaultImgUrl = "https://om.envchina.com/oss";//图片地址（图片地址前缀配置 *选填）
```

3）框架升级至2.0后，所有接口地址率先从中间平台获取，本地配置均为备用地址。

项目开发前修改app中间平台唯一id（**重要**）:

```
public final static String appId = "00";//中间平台appId
```

项目初始化时，调用app中间平台配置请求（参考框架代码的`ShowCase_InitActivity`类）：

```
FrmGetMidUrlTask task = new FrmGetMidUrlTask(MidURL_ID, this);
task.start();
```

### 2.3.1应用参数基本设置

`com.sinoyd.frame.config.FrmKeysConfig`文件中
框架定义了默认保留的键名，如`UserGuid，UserName，UserAvatar`等，个性化配置时可以在该类中新增项目需要使用的键名。框架定义键**不允许**修改。

```
public static final String UserGuid = "SINOYD_KEY_UserGuid";//用户ID
public static final String UserName = "SINOYD_KEY_UserName";//用户名
public static final String UserAvatar = "SINOYD_KEY_UserAvatar";//用户头像
public static final String RoleId = "SINOYD_KEY_RoleId";//roleId
public static final String OrgId = "SINOYD_KEY_OrgId";//组织ID
public static final String OrgName = "SINOYD_KEY_OrgName";//组织名称
public static final String UserToken = "SINOYD_KEY_UserToken";//用户token
public static final String ISLogin = "SINOYD_KEY_ISLogin";//登陆标志
public static final String LastUrl = "SINOYD_KEY_LastUrl";//上次从中间平台获取的接口地址
public static final String LastH5 = "SINOYD_KEY_H5";//上次从中间平台获取的H5地址
public static final String IsFirstOpen = "SINOYD_KEY_IsFirstOpen";//是否第一次打开app
```

对于应用中的一些常量与常用参数，框架采用`sqllite`方式保存在本地，并且提供了整合方法。使用方法如下：

- 保存常量

```
//保存用户token
FrmDBService.setConfigValue(FrmKeysConfig.UserToken, token);
```

- 获取常量

```
//获取用户token
FrmDBService.getConfigValue(FrmKeysConfig.UserToken);
```

<font color="grey">**注：**由于采用的是sqllite的方式，应用中保存在本地的参数常量不会随app被杀死而清除，需要清除时请手动操作，有别于一般的缓存SoftReference，使用时请注意。</font>

## 2.4  框架Activity介绍

一般新建的Activity都需要继承`SinoBaseActivity`。`SinoBaseActivity`继承自`BaseActivity`。

框架Activity初始化时加载`frmbase.xml`布局文件，设置默认标题，并且固定屏幕为竖。

`com.sinoyd.frame.actys.SinoBaseActivity`

| 返回类型            | 方法                         | 说明                                                         |
| ------------------- | ---------------------------- | ------------------------------------------------------------ |
| `void`              | `setLayout(View view)`       | 设置布局。初始化提示信息控件。                               |
| `void`              | `setDefaultTitle()`          | 将从上一个页面传递过来"viewtitle"字符串设置为标题。在`onCreate`方法中已调用。 |
| `void`              | `showNetStatus()`            | 显示网络超时状态视图                                         |
| `void`              | `initNB()`                   | 初始化导航栏样式。                                           |
| `BaseActivity`      | `getBaseActivity()`          | 获取`BaseActivity`上下文。                                   |
| `void`              | `showLoading()`              | 显示框架loading图标。                                        |
| `void`              | `hideLoading()`              | 隐藏框架loading图标。                                        |
| `void`              | `showProgress()`             | 显示框架loading图标。。                                      |
| `void`              | `hideProgress()`             | 隐藏框架loading图标。                                        |
| `void`              | `setLayout(int  layoutId)`   | 设置布局文件。                                               |
| `Context`           | `getContext()`               | 获取上下文。                                                 |
| `Activity`          | `getActivity()`              | 获取上下文。                                                 |
| `void`              | `onNBBack()`                 | 点击返回事件。关闭当前Activity。                             |
| `void`              | `onNBRight()`                | 导航栏右上角按钮事件。空方法。                               |
| `View`              | `getRootView()`              | 获取跟布局`frmbase.xml`对象。                                |
| `InfoStatusItem`    | `getStatusItem()`            | 获取状态提示界面的对象。                                     |
| `BaseNavigationBar` | `getNbBar()`                 | 获取导航栏控件对象。                                         |
| `NbImageView`       | `nbBack`                     | 返回控件。                                                   |
| `NbImageView`       | `nbRight`                    | 右上角图片按钮。                                             |
| `NbTextView`        | `nbRightText`                | 右上角文字按钮。                                             |
| `TextView`          | `nbTitle`                    | 顶部标题。                                                   |
| `RelativeLayout`    | `root`                       | 导航栏根布局。                                               |
| `void`              | `hide()`                     | 隐藏导航栏。                                                 |
| `void`              | `show()`                     | 显示导航栏。                                                 |
| `void`              | `addNBCustomView(View view)` | 添加自定义标题栏布局。                                       |
| `View`              | `getNBCustomView()`          | 获取自定义标题栏布局。                                       |
| `void`              | `setNbBackImage(int resid)`  | 设置返回按钮的背景图片。                                     |
| `void`              | `setNBBackground(int resid)` | 设置导航栏的背景图片。                                       |

 

## 2.5  框架Task使用介绍

目前框架提供了`BaseTask `作为异步请求基类，`BaseTask` 继承自`Runnable`。

`com.sinoyd.frame.task.BaseTask`

#### 使用场景

使用Task类的场景适用于所有耗时操作，包括普通HTTP请求，Post提交，webservice调用，本地数据库增删改查。目的是通过多线程调用，避免在主线程调用造成的页面假死，未响应等情况。另一方面，将业务逻辑操作与UI进行剥离，提供代码的复用。

#### 使用示例

```
1. 自定义Task类，继承BaseTask类

2. 在Task类中定义public类型的变量用于请求参数

3. 在execute()方法添加相关网络请求，return接口返回的数据进行UI回调操作。

4. Activiy里声明调用Task，初始化参数以及BaseTask.BaseTaskCallBack接口的实现
```


自定义Task示例：

```
/**
 * 作者： 王一凡
 * 创建时间： 2017/9/11
 * 版权： 江苏远大信息股份有限公司
 * 描述： 角色切换网络请求
 */
public class YW_ChangeRoleTask extends BaseTask {
    public String staff_id;

    public YW_ChangeRoleTask(int taskId, BaseTaskCallBack callBack){        
        super(taskId, callBack);
    }

    @Override
    public Object execute() {
        String method = "hop";
        JsonObject paras = new JsonObject();
        paras.addProperty("staff_id", staff_id);
        Object obj = FrmCommonAction.request(paras, method, FrmCommonAction.POST);
        return obj;
    }
}

```

声明调用Task：

```
YW_ChangeRoleTask task =  new YW_ChangeRoleTask(ChooseTask_ID, YW_ChooseRoleActivity.this);
task.staff_id = roleId;
task.start();
```

声明接收Task返回数据：

```
@Override
public void refresh(final int taskId, final Object obj) {
    hideLoading();
    if(JsonHelp.checkResult(obj)){
		if(taskId == ChooseTask_ID) {
             //操作返回的数据obj
		}
	}
}
```



## 2.6 本地文件管理

框架升级至2.0后，本地文件存储结构统一分割为三部分:

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/files.png)

当应用初始化时框架会在本地生成`sinoyd`根目录及`download，log，upload`子目录，分别对应下载文件目录，应用日志目录，上传文件临时目录。

另外，文件路径后加上了**中间平台唯一id标识**，方便开发人员区分本地项目文件。

`AppUtil`类增加三个获取文件路径快捷方法，开发人员在操作本地文件时应根据文件用途加以区分
获取下载文件目录：

```
AppUtil.getDownloadFolderPath();
```

获取下载文件目录：

```
AppUtil.getUploadFolderPath();
```

获取应用日志目录:

```
AppUtil.getLogFolderPath();
```



## 2.7  框架相关SDK

### 2.7.1程序主控制类

`com.sinoyd.frame.action.FrmCommonAction`


| 返回类型     | 方法                                                         | 说明                                                         |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `boolean`    | `isUserLogin()`                                              | 获取用户登陆状态                                             |
| `void`       | `setUserLogin()`                                             | 设置用户登陆状态-已登录                                      |
| `void`       | `setUserLogout()`                                            | 设置用户登陆状态-登出  清空用户本地数据：  UserToken、UserName、RoleId |
| `String`     | `getUserToken()`                                             | 获取当前token                                                |
| `boolean`    | `isFirstOpen()`                                              | 判断用户是否第一次打开系统                                   |
| `boolean`    | `setFirstOpen()`                                             | 设置用户已打开系统                                           |
| `JsonObject` | `request(JsonObject paras,String method,  int requestType)`  | 基于OKHttp的网络请求通用方法  <br/>@param paras 请求携带参数  <br/>@param method请求方法名称  <br/>@param requestType 网络请求类型POST/GET/PUT/DELETE |
| `JsonObject` | `request(JsonObject paras,String method,  String url  int requestType)` | 基于OKHttp的网络请求通用方法  <br/>@param paras 请求携带参数  <br/>@param method请求方法名称  <br/>@param method请求地址  <br/>@param requestType 网络请求类型POST/GET/PUT/DELETE |
| `JsonObject` | `uploadFile(String method, HashMap<String, String> params, File file, String mimeType)` | 基于OKHttp的附件上传方法 <br/>@param method请求方法名称  <br/>@param params附件携带参数（键值对） <br/>@param file等待上传文件 <br/>@param mimeType文件类型（可忽略） |

### 2.7.2网络请求工具类

- ~~`com.sinoyd.frame.util.HttpUtil`~~

此类基于`org.apache.http.legacy`打造，网络协议是`Http/Restful`方式，如有项目涉及`WebService`或其他网络协议，请联系框架开发人员。**`API23`（`Android6.0`）后官方已不再提供apache相关支持，所以该类及内含方法已过时，非必要特殊场景避免使用**。

| 返回类型     | 方法                                                    | 说明                                                         |
| ------------ | ------------------------------------------------------- | ------------------------------------------------------------ |
| `void`       | `trustAllHosts()`                                       | 信任所有主机（应用于https地址的请求验证）                    |
| `String`     | `dealWithBs(String bs)`                                 | 处理异常返回，防止json解析出错                               |
| `String`     | `cnToUnicode(String str)`                               | 中文转为ASCII编码（用于参数请求）                            |
| `String`     | `Convert(String str)`                                   | ASCII编码转化为中文（用于Task返回值接收）                    |
| `String`     | `cn2Unicode(String str)`                                | 中文编码转化为ASCII（用户Task发送参数时转换）                |
| `JsonObject` | `request(String httpurl, String data, int requestTyoe)` | 框架网络请求方法 <br/> @param httpurl 请求地址 <br/> @param data请求参数  <br/> @param requestType 网络请求类型POST/GET/PUT/DELETE |

- `com.sinoyd.frame.util.OKHttpUtil`

框架升级至2.0后原底层所有网络交互方法已迁移至此类，基于`okhttp4`开发，整合了参数封装、数据回调逻辑。

| 返回类型           | 方法                                                         | 说明                                                         |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `this`             | `OKHttpUtil()`                                               | 构造函数                                                     |
| `JsonObject`       | `request(String httpurl,String data,   int requestTyoe)`     | 框架网络请求方法  <br/>@param httpurl 请求地址  <br/>@param data请求参数  <br/>@param requestType 网络请求类型POST/GET/PUT/DELETE |
| `JsonObject`       | `postFile(String uploadUrl, Map<String, String> params, File file)` | 上传附件方法  <br/>@param httpurl 请求地址  <br/>@param params附件携带参数参数  <br/>@param file 待上传文件 |
| `FormBody.Builder` | `getFormData(String params, FormBody.Builder builder)`       | 拼装form-data请求参数  <br/>@param params 请求参数  <br/>@param builder 参数构造对象 |
| `JsonObject`       | `getResultData(int responseCode, String result)`             | 拼装http响应回调数据  <br/>@param responseCode http响应码  <br/>@param result 接口返回字符串数据 |
| `JsonObject`       | `getErrorResultData()`                                       | 拼装http响应失败回调数据                                     |

### 2.7.3 Json工具类

`com.sinoyd.frame.util.JsonHelp`

| 返回类型    | 方法                                                         | 说明                                                         |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `ArrayList` | `DocumentJson(JsonArray jasonArray,Class<?> class,String  itemTitle)` | 将JsonArray数据解析为ArryList  <br/>@param 待解析的JsonArray数据<br/>@param class 数据实体类型  <br/>@param itemTitle Json数据名称 |
| `Object`    | `DocumentJson(JsonObjectjasonObject,Class<?> class)`         | 将JsonArray数据解析为Object  <br/>@param 待解析的JsonObject数据<br/>@param class 数据实体类型 |
| `boolean`   | `checkResult(Object obj)`                                    | 检查json数据是否符合当前应用的解析规范   <br/>@param obj 需要进行检查的json数据 |

1.转换为`Java`实体类示例：

```
public static YWMainModel getMainInfo(Object object) {
    YWMainModel obj = new YWMainModel();
    try {
        JsonObject jsonObj = (JsonObject) object;
		JsonObject body = (JsonObject) jsonObj.get("body");
        obj = (YWMainModel)JsonHelp.DocumentJson(body,YWMainModel.class); 
    } catch (Exception e) {
        e.printStackTrace();
    }
    return obj;
}
```

2.转换为`ArrayList<实体类>`示例：

```
public static List<YWPotModel> getPotListInfo(Object object) {
    List<YWPotModel> mlsit = new ArrayList<>();
    try {
        JsonObject jsonObj = (JsonObject) object;
        JsonObject body = (JsonObject) jsonObj.get("body");
        if (JsonArray.class == body.get("data").getClass()) {
            JsonArray dataArray = body.getAsJsonArray("data");
            mlsit= JsonHelp.DocumentJson.(dataArray, YWPotModel.class, "");
        }
    } catch (Exception e) {
        e.printStackTrace();
    }
    return mlsit;
}
```

### 2.7.4 日期工具类

`com.sinoyd.frame.util.DateUtil`

| 返回类型 | 方法                                                         | 说明                                                         |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `String` | `switchDay(int day)`                                         | 将数字数字不足2位首位补0。  <br/>@param day                  |
| `String` | `dateStringPattern(String date, String oldPattern, String newPattern)` | 将某String类型日期根据自定义日期格式转换成另一String类型日期  <br/>@param date需要转换的String日期  <br/>@param oldPattern 转换前的日期格式  <br/>@param newPattern 转换后的日期格式 |
| `String` | `getDatePoor(Date endDate, Date nowDate)`                    | 获取时间差。 <br/>@param endDate 截止日期  <br/>@param nowDate 起始日期 |
| `String` | `convertDate(Date date, String format)`                      | 将日期转为指定格式的字符串。格式：年份yyyy，月份MM，日期dd，小时HH，分钟mm，秒ss。  <br/>@param date 日期  <br/>@param format 格式，如：yyyy-MM-dd HH:mm:ss |
| `String` | `getCurrentDateByFormat(String format)`                      | 根据制定日期格式获取String类型日期  <br/>@param format日期格式 |
| `String` | `getCurrentTime()`                                           | 获取格式yyyy-MM-ddHH:mm:ss的当前时间。                       |
| `String` | `getYesterdayDateByFormat(String format)`                    | 获取昨天日期<br/>@param format日期格式                       |
| `String` | `getLastWeekDateByFormat(String format)`                     | 获取上周当天日期<br/>@param format日期格式                   |
| `String` | `getWeekNameByNum(int num)`                                  | 获取指定数字对应的星期几。1到7对应"日"到"六"。               |
| `String` | `getWeekNameByDate(Date d)`                                  | 获取指定日期对应的星期几  <br/>@param d 日期                 |
| `String` | `Num2Haizi_Week(int day)`                                    | 获取指定数字对应的星期几。0到6对应的"星期日"到"星期六"。  <br/>@param day |
| `String` | `Num2Haizi_Week_HTML_Color(int day)`                         | 获取指定数字对应的星期几。0到6对应的"星期日"到"星期六"。星期日和星期六带有红色字体的html标签。 |
| `Date`   | `convertString2Date(String str, String formatStr)`           | 将定制格式的字符换转化为日期类型  <br/>@param str 日期字符串  <br/>@param formatStr 指定格式 |
| `String` | `getWeekByDate(Date date)`                                   | 获取指定日期对应的星期几。返回汉字，如"星期二"。  <br/>@param date指定日期 |
| `String` | `getWeekByDateSingleChar(Date date)`                         | 获取指定日期对应的星期几。返回汉字，如"二"。  <br/>@param date指定日期 |
| `int`    | `getWeekByDateTime(Date date)`                               | 获取指定日期对应的星期几。0到6对应的星期日到星期六。返回数字。  <br/>@param date指定日期 |
| `String` | `getWeekByDateStr(String dateStr)`                           | 获取指定日期对应的星期几。0到6对应的星期日到星期六。返回汉字，如"星期二"。  <br/>@param dateStr指定日期字符串，格式必须为"yyyy-MM-dd" |
| `String` | `getWeekByDate_HTML_Color(Date date)`                        | 获取指定日期对应的星期几。返回汉字，如"星期二"，如果是周末加上红色字体的html标签。  <br/>@param date指定日期 |
| `String` | `getWeekByFormatedDateStr(String s)`                         | 获取指定日期对应的星期几。返回汉字，如"星期二"。 <br/>@param s指定日期，格式必须为yyyy-MM-dd。 |
| `String` | `getWeekByFormatedDateStr_HTML_Color(String s)`              | 获取指定日期对应的星期几。返回汉字，如"星期二"。如果是周末加上红色字体的html标签。 <br/>@param s指定日期，格式必须为yyyy-MM-dd。 |
| `int`    | `compareDateTime(String date1, String date2)`                | 比较2个日期大小。大于0则date1晚于date2，等于0则相同<br/>@param date1  <br/>@param date2 |

### 2.7.5日期选择工具类

`com.sinoyd.frame.util.ScheduleUtil`

| 返回类型 | 方法                                                         | 说明                                                         |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `void`   | `chooseDate(Context con, final View v, Date date, final ChooseDate callback)` | 弹出日期选择框  <br/>@param v需要写入的textview  <br/>@param date默认选中日期  <br/>@param callback回调方法 |
| `void`   | `chooseDateAndTime(final Context con, final View[] v, Date date, final ChooseDate callback)` | 弹出日期时间选择框  <br/>@param v需要写入的textview  <br/>@param date默认选中日期  <br/>@param callback回调方法 |
| `void`   | `chooseDateByFormat(final Context con, final View[] v, Date date, final String format, final ChooseDate callback)` | 弹出日期选择框，按要求格式返回  <br/>@param v需要写入的textview  <br/>@param date默认选中日期  <br/>@param format需要返回的日期格式，如yyyy-MM-dd<br/>@param callback回调方法 |



### 2.7.6 IO工具类

- `com.sinoyd.frame.util.IOHelp`输入/输出工具处理类

| 返回类型  | 方法                                                         | 说明                                                         |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `String`  | `File2Base64(File f)`                                        | 将文件转成base64字符串。  <br/>@param f 本地文件对象         |
| `byte[]`  | `Bitmap2Bytes(Bitmap bm)`                                    | 将Bitmap转为字节数组。  <br/>@param bm                       |
| `byte[]`  | `obj2bytes(Object obj)`                                      | 将Object转为字节数组。  <br/>@param obj                      |
| `Object`  | `bytes2obj(byte[] b)`                                        | 将字节数组转为Object对象。  <br/>@param b                    |
| `void`    | `TextFileContinueWrite(String path, String log)`             | 向一个文本中续写数据。  <br/>@param path 文件路径  <br/>@param log 数据内容 |
| `byte[]`  | `InputStreamToByte(InputStream is)`                          | 将流转为字节数组。  <br/>@param is                           |
| `byte[]`  | `File2Byte(File f)`                                          | 将本地文件转为字节数组。 <br/>@param f 本地文件对象          |
| `void`    | `FoldCreate(String path)`                                    | 创建指定目录。 <br/>@param path 目录                         |
| `void`    | `deleteFile(File file)`                                      | 删除文件或文件夹。  <br/>@param file 文件或文件夹对象        |
| `void`    | `copyFile(String assfilename, String destpathname)`          | 拷贝文件。  <br/>@param assfilename 目标文件路径  <br/>@param destpathname 拷贝路径 |
| `String`  | `readtxt(String path)`                                       | 读取文件内容。  <br/>@param path 文件路径                    |
| `void`    | `writeText2Path(String path, String msg)`                    | 向目标文本中写入数据，原数据会被覆盖。  <br/>@param path 文件路径  <br/>@param msg 数据内容 |
| `boolean` | `saveFile(byte[] b, String filepath)`                        | 将字节数组保存到指定文件。路径不存在会自动创建，文件已存在会覆盖。保存成功返回true，否则返回false。  <br/>@param b 字节数组  <br/>@param filepath 文件路径 |
| `void`    | `byte2file(byte[]  b, String filepath)`                      | 同saveFile方法。                                             |
| `void`    | `copyFileTemp(String src, String dest)`                      | 将目标文件拷贝至指定文件中。  <br/>@param src 目标文件路径 <br/>@param dest 指定的文件夹路径 |
| `void`    | `copyFileFromAss2Dir(Context con, String assfilename, String destpathname)` | 从assets拷贝文件到指定文件夹中。  <br/>@param con 上下文  <br/>@param assfilename assets中的文件路径  <br/>@param destpathname指定的文件夹路径 |
| `String`  | `do_exec(String cmd)`                                        | 执行cmd命令并返回结果。  <br/>@param cmd 命令语句            |
| `String`  | `throwException2String(Throwable ex)`                        | 将异常转为字符串。  <br/>@param ex 异常对象                  |
| `byte[]`  | `toByteArray(Object o)`                                      | 同obj2bytes方法。                                            |
| `Object`  | `toObject(byte[] bytes)`                                     | 同bytes2obj方法。                                            |
| `String`  | `getMIMEType(File file)`                                     | 获取文件MimeType值。<br/>@param file 文件对象                |
| `String`  | `getFileExtension(File file)`                                | 获取文件后缀名。（去除文件名后缀参数）<br/>@param file 文件对象 |
| `String`  | `getFileNameByUrl(String url)`                               | 根据文件路径获取文件名。<br/>@param url文件路径（可以是网络路径，也可以是本地路径） |
| `double`  | `getDirSize(File file)`                                      | 获取指定文件或文件夹大小。单位M。  <br/>@param file 文件对象 |
| `long`    | `getFileSize(File file)`                                     | 获取指定文件大小。单位byte。<br/>@param file 文件对象        |
| `String`  | `getPrintSize(long size)`                                    | 转换文件大小(KB/MB/GB)。<br/>@param size 文件byte大小        |
| `Bitmap`  | `getImgByFileName(Context context, String filename)`         | 根据文件类型获取文件图标。<br/>@param context 上下文 <br/>@param filename文件名 |
| `String`  | `decodeFile(String srcPath)`                                 | 压缩图片文件，返回压缩后图片的本地路径。<br/>@param srcPath 待压缩图片路径 |
| `String`  | `decodeFileFromIO(Activity activity, Intent data)`           | 从系统流中获取文件，返回文件本地路径。<br/>@param activity 上下文 <br/>@param data系统数据流 |

- `com.sinoyd.frame.util.IOService`输入/输出工具服务类

| 返回类型  | 方法                                                         | 说明                                                         |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `boolean` | `checkNet(Context context)`                                  | 检查网络连接。<br/>@param context 上下文                     |
| `void`    | `AlertWithLayout(Context con, int layout, String title)`     | 弹出自定义窗口。<br/>@param con 上下文<br/>@param layout 自定义布局<br/>@param title 弹出窗标题 |
| `void`    | `Call(Context con, String phonenum)`                         | 发起电话呼叫。<br/>@param con 上下文<br/>@param phonenum 电话号码 |
| `void`    | `SendMsg(Context con, String phonenum, String shortmsg)`     | 调起发送短信界面。<br/>@param con 上下文<br/>@param phonenum 电话号码<br/>@param shortmsg 短信内容 |
| `void`    | `openCamera(Activity activity, String filePath)`             | 打开系统相机并回调至页面。<br/>@param activity 页面对象 <br/>@param filePath 照片文件存放路径 |
| `void`    | `openPic(Activity activity)`                                 | 打开系统相册并回调至页面。<br/>@param activity 页面对象      |
| `void`    | `openSoundRecoder(Activity activity)`                        | 打开系统录音并回调至页面。  <br/>@param activity 页面对象    |
| `void`    | `openCameraVideo(Activity activity)`                         | 打开系统视频拍摄并回调至页面。  <br/>@param activity 页面对象 |
| `void`    | `openPicMulti(Activity activity)`                            | 打开图片多选并回调至页面。  <br/>@param activity 页面对象    |
| `void`    | `openFile(Context con, File file)`                           | 打开系统文件。  <br/>@param con 上下文<br/>@param file 待打开文件 |
| `void`    | `playMusic(Context con, String filename)`                    | 播放媒体文件。<br/>@param con 上下文<br/>@param filename 文件对象 |
| `void`    | `startApp(Context con, String packageName, String className, String param)` | 跳转至三方应用某页面<br/>@param con 上下文<br/>@param packageName 应用包名<br/>@param className 跳转页面类名<br/>@param param 携带参数 |
| `void`    | `startApp(Context con, String packageName, String param)`    | 跳转至三方应用<br/>@param con 上下文<br/>@param packageName 应用包名<br/>@param param 携带参数 |

<font color="grey">**注：**此工具类增加了若干个以fragment为对象的同名异构方法，目的是为了回调函数onActivityResult()可以直接在fragment页面进行使用，方法构造相同，故不在此处一一列举。</font>


### 2.7.7反射工具类

`com.sinoyd.frame.util.ResManager`

| 返回类型 | 方法                                                 | 说明                                                         |
| -------- | ---------------------------------------------------- | ------------------------------------------------------------ |
| `int`    | `getResourseIdByName(String className, String name)` | 根据资源名称获取资源Id  <br/>@param className文件夹名  <br/>@param name文件名 |
| `int`    | `getLayoutInt(String layoutname)`                    | 返回`R.layout.layoutname`  <br/>@param layoutname 文件名     |
| `int`    | `getStringInt(String stringname)`                    | 返回`R.string.stringname`  <br/>@param stringname资源名      |
| `int`    | `getIdInt(String idname)`                            | 返回`R.id.idname`  <br/>@param idname 控件id                 |
| `int`    | `getDrawableInt(String drawablename)`                | 返回`R.drawable.drawablename`  <br/>@param drawablename      |
| `int`    | `getAttrInt(String attrname)`                        | 返回`R.attr.attrname`  <br/>@param attrname                  |
| `int`    | `getAnimInt(String animname)`                        | 返回`R.anim.animname`  <br/>@param animname                  |
| `int`    | `getRawInt(String rawname)`                          | 返回`R.raw.rawname`  <br/>@param rawname                     |
| `int`    | `getColorInt(String colorname)`                      | 返回`R.color.colorname`  <br/>@param colorname               |
| `int`    | `getStyleInt(String stylename)`                      | 返回`R.style.stylename`  <br/>@param stylename               |
| `int`    | `getAnimatorInt(String animatorname)`                | 返回`R.animator.animatorname`  <br/>@param animatorname      |

### 2.7.8日志工具类

`com.sinoyd.frame.util.LogUtil`

| 返回类型 | 方法                                     | 说明                                                         |
| -------- | ---------------------------------------- | ------------------------------------------------------------ |
| `void`   | `frm_log(Class cls, String log)`         | 控制台输出日志。  <br/>@param cls 类名  <br/>@param log 日志内容 |
| `void`   | `writeLogThread(String tag, String log)` | 使用Thread线程写入日志  <br/>@param tag 标签  <br/>@param log 日志内容 |
| `void`   | `Log2Storage(String log)`                | 将日志保存本地文件。  <br/>@param log 日志内容               |

### 2.7.9像素工具类

`com.sinoyd.frame.util.DensityUtil`

| 返回类型            | 方法                                 | 说明                                                       |
| ------------------- | ------------------------------------ | ---------------------------------------------------------- |
| `int`               | `dip2px(Context con, float dpValue)` | dip转px  <br/>@param con 上下文  <br/>@param dpValue dip值 |
| `int`               | `px2dip(Context con, float pxValue)` | px转dip  <br/>@param con 上下文  <br/>@param pxValue px值  |
| `public static int` | `px2sp(Context con, float pxValue)`  | px转sp  <br/>@param con 上下文  <br/>@param pxValue px值   |
| `public static int` | `sp2px(Context con, float spValue)`  | sp转px  <br/>@param con 上下文  <br/>@param spValue sp值   |

### 2.7.10设备工具类

`com.sinoyd.frame.util.PhoneUtil`

| 返回类型  | 方法                                                         | 说明                                                         |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `boolean` | `ExistSDCard()`                                              | 判断系统SD卡是否正常挂载。（/mnt/sdcard目录是否存在）        |
| `String`  | `getDeviceId(Context con)`                                   | 获取当前移动终端的唯一标识。如果是GSM网络，返回IMEI；如果是CDMA网络，返回MEID。如果都为空或没有权限则返回mac地址。  <br/>@param con 上下文 |
| `String`  | `getMacAddress(Context con)`                                 | 获取设备mac地址  <br/>@param con上下文                       |
| `int`     | `getPhoneWidth(Context con)`                                 | 获取设备宽度  <br/>@param con上下文                          |
| `int`     | `getPhoneHeight(Context con)`                                | 获取设备高度  <br/>@param con上下文                          |
| `void`    | `invokeSystemBrowser(Context con, String url)`               | 用系统浏览器打开指定网址。  <br/>@param con上下文  <br/>@param url 网址 |
| `void`    | `sendMsgUsePhoneSelf(Context con, String phonenum, String body)` | 打开编辑短信界面。  <br/>@param con上下文  <br/>@param phonenum 对方号码  <br/>@param body 短信内容 |
| `boolean` | `isTablet(Context con)`                                      | 判断当前设备是否是平板。  <br/>@param con上下文              |
| `void`    | `cancelAllNotify(Context con)`                               | 去除通知栏通知  <br/>@param con上下文                        |

### 2.7.11应用工具类

`com.sinoyd.frame.util.AppUtil`

| 返回类型      | 方法                                 | 说明                                            |
| ------------- | ------------------------------------ | ----------------------------------------------- |
| `Application` | `getApplicationContext()`            | 获取系统context对象                             |
| `String`      | `getStoragePath()`                   | 获取本地文件存放根路径                          |
| `String`      | `getFolderPath(String folder)`       | 获取指定文件夹路径<br/>@param folder 文件夹名称 |
| `String`      | `getDownloadFolderPath()`            | 获取下载文件夹路径                              |
| `String`      | `getUploadFolderPath()`              | 获取上传文件夹路径                              |
| `String`      | `getLogFolderPath()`                 | 获取日志文件夹路径                              |
| `int`         | `getTitleBarHeight(Context context)` | 获取框架标题栏高度<br/>@param context 上下文    |
| `String`      | `md5(String string)`                 | 字符MD5加密<br/>@param string 需要加密字符串    |
| `PackageInfo` | `getPackageInfo(Context con)`        | 获取当前app的信息。  <br/>@param con上下文      |
| `String`      | `getPackageName(Context con)`        | 获取当前app的包名。  <br/>@param con上下文      |
| `String`      | `getAppVersion()`                    | 通过系统对象，获取当前app的版本号。             |
| `String`      | `getVersionName(Context con)`        | 获取当前app的版本号。  <br/>@param con上下文    |

### 2.7.12下载工具类

`com.sinoyd.frame.util.DownloadUtil`

| 返回类型       | 方法                                                         | 说明                                                         |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `this`         | `DownloadUtil(Context con, String urlStr, DownloadCallback callback)` | 普通文件下载  <br/>@param con 上下文  <br/>@param urlStr 文件网络地址<br/>@param callback 下载完成回调 |
| `this`         | `DownloadUtil(Context con, String urlStr, String folderPath, DownloadCallback callback) ` | 普通文件下载(指定本地路径)  <br/>@param con 上下文  <br/>@param urlStr 文件网络地址  <br/>@param folderPath 自定义文件保存路径  <br/>@param callback 下载完成回调 |
| `this`         | `DownloadUtil(Context con, String urlStr, String filename, String fileType, DownloadCallback callback)  ` | 普通文件下载(指定文件名)  <br/>@param con 上下文  <br/>@param urlStr 安装包网络地址<br/>@param filename 自定义文件名<br/>@param callback 下载完成回调 |
| `DownloadUtil` | `setCancelable(boolean cancelable)`                          | 设置下载是否可中断  <br/>@param cancelable 标志位            |
| `void`         | `run()`                                                      | Thread run方法重载，执行下载逻辑                             |

 

**注**：进行下载业务时，调用`DownloadUtil`方法如下：

```
new DownloadUtil(getContext(), versionModel.getDownLoadUrl(), null).start()
```



## 2.8通用模块与组件

### 2.8.1 框架标题栏控制

框架集成了标题栏及标题栏的按钮功能操作，开发者在页面开发过程中不需要自己定义。

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/t2.png)

 以下为开发步骤：

1）创建的Activity继承`SinoBaseActivity`

```
  public class DemoActivity extends SinoBaseActivity {}  
```

2）设置标题

```
getNbBar().setNBTitle(“任务详情”);  `
```

3）隐藏/显示左侧返回按钮

```
getNbBar().nbBack.setVisibility(View.GONE);//隐藏
getNbBar().nbBack.setVisibility(View.VISIBLE);//显示
```

4）设置右侧按钮文字

```
getNbBar().nbRightText.setText("保存");
getNbBar().nbRightText.setVisibility(View.VISIBLE);
```

5）设置标题栏右侧图标按钮（单图标）

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/t3.png)

```
getNbBar().nbRight.setImageResource(R.drawable.frm_sacn_btn);
getNbBar().nbRight.setVisibility(View.VISIBLE);
```

6）设置标题栏右侧自定义布局（多图标/文字）

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/t1.png)


```
LinearLayout titleright = (LinearLayout)LayoutInflater.from(getContext()).inflate(R.layout.yw_formright_layout, null);//自定义布局
getNbBar().navRightCustom.addView(titleright);//添加布局
getNbBar().navRightCustom.setVisibility(View.VISIBLE);
```

7）重写`onNBRight`方法，实现右侧按钮点击事件

```
@Override
public void onNBRight() {
    super.onNBRight();
	//执行业务逻辑
}
```

**注**：1.如需要隐藏标题栏，调用下例方法：

```
getNbBar().hide();
```

2.标题栏左侧图标默认为返回按钮，点击事件为关闭页面。如需自定义请参考本文“**2.4框架Activity介绍**”，在`SinoBaseActivity`介绍中列举了针对左右两侧图标修改的相关方法。

 

### 2.8.2 Glide图片异步加载

开发框架升级至2.0版本后，图片加载库已从universal-image-loader变更为效率更高、内存占用更少的`glide4`

代码示例：

```
Glide.with(this.mContext)
.load(imageFile)
.placeholder(R.drawable.frm_default_error)
.error(R.drawable.frm_default_error)
.centerCrop()
.into(this.image);
```

- `placeholder`：图片loading样式，框架提供默认图片
- `error`：图片加载异常样式，框架提供默认图片
- `centerCrop`：图片填充模式，另外提供`fitCenter`、`circleCrop`等填充类型，开发时根据项目具体需求调整
- `into`：视图加载对象



### 2.8.3 圆角图片

  ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/image014.png)

布局文件中使用`RoundedImageView`控件即可。用法和`Imageview`控件类似。

```
<com.sinoyd.frame.views.roundimageview.RoundedImageView
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/roundImageView"
    android:layout_width="100dp"
    android:layout_height="100dp"
    android:layout_centerHorizontal="true"
    android:layout_marginTop="10dp"
    android:scaleType="centerCrop"
    app:border_color="@color/black"
    app:border_width="1dip"
    app:mutate_background="true"
    app:oval="true" />
```



### 2.8.4 通用搜索

  ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/t5.png)

1）layout布局文件添加控件

```
<include layout="@layout/frmsearchbar"/> 
```

2）activity中注册搜索框

```
//注册搜索框   
new FrmSearchBar(getRootView(), this); 
```

3）监听搜索事件，activity实现`FrmSearchBar.SearchActionListener`接口

```
@Override   
public void search(String keyWord) {     
	this.keyWord = keyWord.trim();    
	//业务逻辑处理   
} 
```


### 2.8.5 IOS风格弹出菜单

  ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/sheet.png)

 

1）给界面添加主题

```
  getActivity().setTheme(R.style.ActionSheetStyleIOS7);  
```

2）实现`FrmActionSheet.MenuItemClickListener`接口，重写`onItemClick`方法

```
 @Override
public void onItemClick(int position) {
    ToastUtil.showShort(this,”点击了第” + position + ”个元素”);
}
```


3）在点击事件中弹出菜单

```
@OnClick(R.id.btn_add)
public void onClick() {
    FrmActionSheet menuView = new FrmActionSheet(getActivity());
    menuView.setCancelButtonTitle("取消");
    menuView.addItems("相册", "相册（多选）", "拍照", "录音", "录像");
    menuView.setItemClickListener(this);
    menuView.setCancelableOnTouchMenuOutside(true);
    menuView.showMenu();
}
```



### 2.8.6 IOS风格CheckBox

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/image017.png)

1）layout布局文件中添加控件

```
<com.sinoyd.frame.views.togglebutton.ToggleButton
   android:layout_marginLeft="20dp"
   android:layout_width="54dp"
   toggle:onColor="#f00"
   toggle:offColor="#ddd"
   toggle:spotColor="#00f"
   toggle:offBorderColor="#000"
   toggle:borderWidth="2dp"
   android:layout_height="30dp" >
 </com.sinoyd.frame.views.togglebutton.ToggleButton>
```

2）初始化并监听事件

```
toggle.setOnToggleChanged(new ToggleButton.OnToggleChanged() {
    @Override
    public void onToggle(boolean on) {
        ToastUtil.showShort(this,”开关状态” + on)
    }
});
```



### 2.8.7 支持过度滑动ScrollView

原则上，在开发者使用框架开发项目的过程中，凡涉及到垂直滑动的页面都需要使用`FrmOverScrollView`控件替代原生`ScrollView`，不仅是为了统一公司移动应用的风格，也是为了提升用户的交互体验。

对于一些页面复杂的应用场景，如遇到滑动冲突问题，可暂时不使用该控件，及时通知框架开发人员。

```
<com.sinoyd.frame.views.FrmOverScrollView
    android:layout_height="match_parent"
    android:layout_width="match_parent"
    <LinearLayout .../>
</com.sinoyd.frame.views.FrmOverScrollView>
```



### 2.8.8 栏目选择控件

  ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/image018.png)

1）实现`RadioGroup.OnCheckChangeListener`接口，重写`onItemClick`方法

```segmentedGroup.setOnCheckedChangeListener(this);
@Override
public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
     ToastUtil.showShort(this,”点击了第” + position +”个元素”);
}
```

2）在布局文件中声明

```
<com.sinoyd.frame.views.FrmSegmentedGroup
    android:layout_alignParentBottom="true"
    android:layout_centerHorizontal="true"
    android:id="@+id/segmented_group"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginTop="5dp"
    android:layout_marginBottom="5dp"
    android:orientation="horizontal"
    segmentedgroup:sc_border_width="1dp"
    segmentedgroup:sc_corner_radius="5dp"
    segmentedgroup:sc_tint_color="#1e90ff"
    segmentedgroup:sc_checked_text_color="#ffffff"
    android:layout_gravity="center_horizontal">
    <RadioButton
        android:id="@+id/button_default"
        android:layout_width="100dp"
        android:layout_height="wrap_content"
        android:text="默认分组"
        style="@style/RadioButton" />
    <RadioButton
        android:id="@+id/button_type"
        android:layout_width="100dp"
        android:layout_height="wrap_content"
        android:text="按类型分组"
        style="@style/RadioButton" />
    <RadioButton
        android:id="@+id/button_instrument"
        android:layout_width="100dp"
        android:layout_height="wrap_content"
        android:text="按仪器分组"
        style="@style/RadioButton" />
</com.sinoyd.frame.views.FrmSegmentedGroup>
```



### 2.8.9 滚动图片广告控件

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/image019.png)

1）将广告图片地址赋值给当前控件`setupLayoutByImageUrl(URL_LIST)`，调用show() 方法将其展示

```
this.indicate_view.setupLayoutByImageUrl(URL_LIST);
this.indicate_view.show();
```

2.实现`ImageIndicatorView.OnItemClickListener`接口，重写`onPosition`方法

```
indicate_view.setOnItemChangeListener(this);  
```

3.实现`ImageIndicatorView.OnItemChangeListener`接口，重写`OnItemClick`方法

```
this.indicate_view.setOnItemClickListener(this);  
```

4.完整示例

```
void initIndicate(){
    indicate_view.setOnItemChangeListener(this);
    List<String> URL_LIST = new ArrayList<>();
    URL_LIST.add(url1);
	URL_LIST.add(url2);
	URL_LIST.add(url3);
    this.indicate_view.setupLayoutByImageUrl(URL_LIST);
    this.indicate_view.setOnItemClickListener(this);
    this.indicate_view.setCurrentItem(1);//默认显示第一页
    this.indicate_view.show();
}
```

4.在布局中声明

```
<com.sinoyd.frame.views.ImageIndicatorView
    android:id="@+id/indicate_view"
    android:layout_width="match_parent"
    android:layout_height="220dp" />
```



### 2.8.10 右滑关闭页面

  ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/slide.png)

 

- 凡继承框架基类`SinoBaseActivity`的页面，即默认开启右滑关闭功能。

- 在首页、地图页面等不需要右滑关闭的功能中，使用下例方法禁用该功能。

```
//关闭右滑关闭功能
openSlideFinish(false);
```



### 2.8.11 列表上拉、下拉刷新

框架使用的列表刷新基于官方`android.support.v4.widget.SwipeRefreshLayout`
考虑到组件的拓展性，框架没有集成自动的列表上拉下拉效果，需要开发者手动添加头部、尾部加载效果和组织列表数据。
**下拉效果：**


 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/up2.png)

**上拉效果：**

  ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/down2.png)

1）layout布局文件中添加控件

```
<android.support.v4.widget.SwipeRefreshLayout
    android:id="@+id/swipeRefreshLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <ListView
        android:id="@+id/lv"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:fadingEdge="none"
        android:overScrollMode="never"/>
</android.support.v4.widget.SwipeRefreshLayout>
```

2）实现`AbsListView.OnScrollListener`接口，初始化`footLoadView`，注册`listview`上拉滚动监听

```
footLoadView = new FrmListFootView(getActivity());
listView.setOnScrollListener(this);
```

```
@Override
public void onScrollStateChanged(AbsListView view, int scrollState) {
    if (scrollState == AbsListView.OnScrollListener.SCROLL_STATE_IDLE) {
        if (view.getLastVisiblePosition() == view.getCount() - 1 &&   view.getCount() >= pageSize * currentPageIndex) {
            //下拉加载更多
            ++page;
			//进行业务操作
        }
    }
}
@Override
public void onScroll(AbsListView view, int firstVisibleItem, int visibleItemCount, int totalItemCount) {

}
```

3）注册`mSwipeLayout`下拉事件监听

```
//mSwipeLayout.setColorSchemeColors(上拉加载动画颜色);//默认黑色
mSwipeLayout.setOnRefreshListener(new SwipeRefreshLayout.OnRefreshListener() {
    @Override
    public void onRefresh() {
        //上拉刷新,初始化数据
        page = 1;
        //进行业务操作
    }
});
```

4）在接口返回方法中进行列表分页效果的操作示例：

```
@Override
public void refresh(int taskId, final Object obj) {
    mSwipeLayout.setRefreshing(false);
    if(JsonHelp.checkResult(obj)){
        if(taskId == GetPotTask_ID){
            if(currentPageIndex == 1) {
                potList.clear();
            }
            potList.addAll(action.getPotListInfo(obj));
            if (potList.size() < pageSize * currentPageIndex) {
                if (listView.getFooterViewsCount() > 0) {
					//移除上拉加载进度条
                    listView.removeFooterView(footLoadView);
                }
            } else {
                if (listView.getFooterViewsCount() < 1) {
					//加载上拉加载进度条
                    listView.addFooterView(footLoadView);
                }
            }

            adapter.setData(potList);
            adapter.notifyDataSetChanged();
        }
    }
}
```



### 2.8.12 列表滑块菜单

框架针对业务场景中出现比较多的列表左滑菜单按钮功能进行了整合

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/leftslide.png)

1）定义`ListView`根布局

```
<com.sinoyd.frame.views.swipelistview.SwipeListView
    android:id="@+id/lv_item_task"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:divider="@color/divider_color"
    android:dividerHeight="0.5px"/>
```

2）定义`ListView`的`Item`子布局并自定义按钮文字样式、宽度

```
<com.sinoyd.frame.views.swipelistview.SwipeItemLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">
    <LinearLayout
        android:id="@+id/ll_item"
        android:layout_width="match_parent"
        android:layout_height="60dp"
        android:orientation="horizontal">
        ···
    </LinearLayout>
    
    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="match_parent">
        <Button
            android:id="@+id/anything"
            android:text="自定义"
            android:textColor="#ffffff"
            android:textSize="16sp"
            android:background="#FFAC0C"
            android:layout_width="100dp"
            android:layout_height="match_parent"/>
        <Button
            android:id="@+id/delete"
            android:text="删除"
            android:textColor="#ffffff"
            android:textSize="16sp"
            android:background="#FF1F00"
            android:layout_width="80dp"
            android:layout_height="match_parent"/>
    </LinearLayout>
</com.sinoyd.frame.views.swipelistview.SwipeItemLayout>
```

3）在`ListView`适配器中注册接口，在Activity中实现：
列表元素单击事件：

```
onClickItem(int position);
```

元素按钮单击事件（按钮顺序位置，item所在列表位置）：

```
onClickBtn(int btn, int position);
```



### 2.8.13 图片多选控件

结合项目实际需要，框架提供附件上传-图片多选功能，并集成了上传原图/压缩图片选项

  ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/multi.png)

1）调用`IOService`工具中的`openPicMulti`方法（对象支持activity或fragment）

```
//相册（多选）
IOService.openPicMulti(this);
```

2）在当前页面`onActivityResult()`函数中接收返回的图片数据，数据中压缩过后的图片已经是完成处理后的路径，**不需要额外处理**。

```
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if(requestCode == IOService.OpenPhotoMulit_REQUESTCODE){
        if (resultCode == RESULT_OK) {
            if (data != null) {
                List<String> path = data.getStringArrayListExtra(MultiImageSelectorActivity.EXTRA_RESULT);
                //执行业务逻辑
            }
        }
    }
}
```

 **注**：如需要调整图片压缩倍率，调整`IOHelp`中的`decodeFile`方法：

```
 float widthLimit = 1080f;// 默认压缩宽度为1080
 float hightLimit = 1920f;// 默认压缩高度为1920
 ···
 bitmap.compress(Bitmap.CompressFormat.JPEG, 90, out)//压缩倍率默认为90%
```



# 第三章   框架第三方类库

## 3.1  Zxing二维码扫描

框架已默认集成第三方（zxing3.2.1）二维码扫描库，使用方法如下：

 ![avatar](https://wyf-wx.oss-cn-shanghai.aliyuncs.com/upload/0framedoc/image024.png)

 1）在当前页面调用CaptureActivity类

```
//打开扫描界面扫描条形码或二维码
Intent openCameraIntent = new Intent(this, CaptureActivity.class);
startActivityForResult(openCameraIntent, gotoScanActivity);
```

 2）在当前页面`onActivityResult()`函数中接收二维码扫描数据

```
//接收二维码扫描返回结果
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (resultCode == RESULT_OK) {
        if(requestCode == gotoScanActivity) {
            Bundle bundle = data.getExtras();
			//返回结果字符串
            String scanResult = bundle.getString("result");
            //执行业务逻辑
        }
    }
}
```

 

# 第四章   文档更新记录

**远大Android工作平台****2.0****版本更新笔记 2020/08/20：**

- 框架导入Aspect开发者工具包：`com.hujiang.aspectjx:gradle-android-plugin-aspectjx`

>需要Gradle Plugin Version:4.0.0以上
>同时建议Gradle Verion:6.1.1以上


- 关于基类：

>基类适配androidx：
>原BaseActivity父类android.app.Acitvity改为androidx.fragment.app.FragmentActivity
>原BaseFragment父类android.app.Fragment改为androidx.fragment.app.Fragment
>支持androidx的api及统一fragment管理，比如：
>Activity页面中嵌套fragment由原先getFragmentManager统一改为getSupportFragmentManager
>Fragment页面中嵌套fragment统一使用getFragmentManager()


- 关于动态权限：

>IOHelp中FoldCreate()、deleteFile()、copyFile()方法增加读写权限判断
>Manifest.permission.READ_EXTERNAL_STORAGE, Manifest.permission.WRITE_EXTERNAL_STORAGE
>IOService类Call()方法增加电话呼叫权限判断
>Manifest.permission.CALL_PHONE
>IOService类SendMsg()方法增加短信发送权限判断
>Manifest.permission.SEND_SMS
>IOService类openCamera()方法增加相机、读写权限判断
>Manifest.permission.WRITE_EXTERNAL_STORAGE, Manifest.permission.CAMERA
>IOService类openPic()方法增加读写权限判断
>Manifest.permission.WRITE_EXTERNAL_STORAGE
>IOService类openSoundRecoder()方法增加系统录音权限判断
>Manifest.permission.RECORD_AUDIO
>IOService类openCameraVideo()方法增加相机、读写权限判断
>Manifest.permission.WRITE_EXTERNAL_STORAGE, Manifest.permission.CAMERA
>IOService中openFile()方法增加读写权限判断
>Manifest.permission.READ_EXTERNAL_STORAGE, Manifest.permission.WRITE_EXTERNAL_STORAGE
>DownloadUti().start()线程执行之前加入读写判断
>Manifest.permission.WRITE_EXTERNAL_STORAGE

- 删除功能及依赖包：

>FrmUploadAction类删除
>hybird目录删除
>BridgeImpl类中uploadAttach()方法删除，H5页面不再支持跳转至原生页面上传附件，建议直接使用容器支持<input>标签选择及上传附件
>去除框架com.nostra13.universalimageloader包依赖，加载图片方式由原来以Glide替代原来ImageLoader方式
>去除框架com.github.bumptech.glide:compiler包依赖
>去除框架com.github.chrisbanes:PhotoView包依赖

- 其他乱七八糟：

> 系统provider命名封装，定义applicationId后不需要开发者手动修改。
> ShowCase主页“列表删除菜单”改为“列表滑块菜单”，左滑菜单现在可根据项目需要自行增加功能按钮。
> FrmMojsFragment类中WebChromeClient增加附件上传响应事件，通过H5页面<input>标签调起拍照及相册图片选择并获取回调上传。
> 新增ShowCase_AttachUploadActivity附件上传示例类，原FrmAttachUploadActivity类及相关适配器、数据实体类已删除，不再作为框架类强制要求使用，开发者参考showcase自行定义。

除以上变更之外，其他`API`及功能变更说明已更新至文档主体。

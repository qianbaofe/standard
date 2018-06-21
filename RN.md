驼峰式：第二个单词首字母大写 <br>
大驼峰式：每个单词的首字母都是大写的<br>
默认是驼峰式

## 一:文件
1：文件夹 全部小写字母 <br>
      例如：page，component，assets<br>

2：js文件 大驼峰式规范 
      页面Page结尾<br>
      工具Util结尾<br>
      原生组件Android||IOS结尾 最后统一导出 <br>
 例如：<br>
       HomePage<br>
       HttpUtil<br>
       WebAndroid||WebIOS=>统一在Web.js里面导出<br>


## 二:变量
### 禁止使用var  
实例变量let<br>
实例常量const<br>
静态属性static<br>

1：全局属性(项目启动即引用)   全部大写<br>
     例如： <br>
     global.WIDTH = deviceWidth;<br>

2：静态属性(局部页面使用,使用才引用) 类型+驼峰式命名<br>
例如：<br>
Array                  a        aNameList<br>
string	           s	     sName<br>
Boolean	           b	     bVisible<br>
Float	           f	     fMoney<br>
Function	          fn	     fnMethod<br>
Int	                  i	      iAge<br>
Object	          o	      oType<br>
Regexp            re	      rePattern(正则表达式)<br>
可变类型	          v	      vObj<br>
例如：<br>
```
引用方式通过 类名+变量名 <br>
CacheData.sPhone = "";
CacheData.sToken = "";
CacheData.oPerson = {};
```

3：类变量(需要更新UI 不需要更新UI)  类型+驼峰式命名 <br>
```
需要更新UI
this.state = {
    bFlag:true,
    sNum:"",
    oPerson:{},
}
不需要更新UI
this.bFlag=true
this.sNum = ""
this.oPerson = {}
```

4:实例变量   _{驼峰式组件名字} <br>
   ```
   this.refs._textInput
   this._scrollView
   ```

## 三:方法
#### 1：静态方法 大驼峰式
```
例如：
Http.Post()
Cache.GetToken()
```
#### 2：功能型 
      can,is,get,set,init,show,hide,query,sort,check,<br>
      名称+业务名称 驼峰式命名<br>
#### 3：动作型 xxxxAction <br>
      由用户触发的操作,第一个函数一定是Action <br>
```
例如：用户点击登录函数调用如下
loginAction(点击事件)->checkData(功能型)->(功能型)->(功能型)->Http.Post(this.state.oUser)
```
#### 4：回调型
##### 1：父子组件间回调 onXXX
```
 例如：
  return (<Parent> 
                   <Son1 sName={this.state.sName} onShowDialog={this.showDialog}/>
                </Parent>)
//子组件使用
//this.props.onShowDialog(this.state.bVisible);
```
##### 2：页面回调 XXXCallBack<br>
2.1:<br>
A navigate B<br>
```
A页面
 loginCallBack =(data)=>{doSometing}
 this.props.navigation.navigate(page,{loginCallBack:this.loginCallBack});

B页面执行
loginCallBack(data)
```

2.2:<br>
A通过回调监听B页面的广播<br>
```
//A页面
 DeviceEventEmitter.addListener('isLogin',(data)=>{
            this.loginCallBack(data)
        });
 //B页面
 DeviceEventEmitter.emit('isLogin', data);
```

## 四:组件化<br>
### 禁止在render方法里面写太多代码<br>
纯组件：独立于事件，业务，每个项目都可以复用。<br>
业务组件：和本项目相关联<br>
页面：都多个业务组件组合<br>

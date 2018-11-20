<center><H1>CodePush热更新切换本地与微软服务</H1></center>

之前测试code-push-server时候将服务端地址写成本地了

操作代码：

```
	code-push login http://192.168.1.100:3000
```
&#160; &#160; &#160; &#160;此后很长一段时间没有使用，并且本地服务代码、数据库都删了

&#160; &#160; &#160; &#160;最近app要启用热更新功能，悲剧了各种操作都显示账号已登录，但是无法进行操作。执行 logout指令提示连接服务器失败。然后各种百度谷歌还是没用，突然想到是不是要删除accessKey就无法认证了，然后本地的登录记录是不是也就无效了

&#160; &#160; &#160; &#160;But `accessKey`在本地存储在哪？找不到。。。然后找code-push在本地安装位置，这个百度有	``/usr/local/bin/lib/node_modules/code-push-click``,然后再查看源码

根据命令最终找到了这个

```
var configFilePath = path.join(process.env.LOCALAPPDATA || process.env.HOME, ".code-push.config");

```
ok, accessKey就在这个位置``.code-push.config``
当前用户目录下显示隐藏文件就能找到这个文件了，打开后可以修改

```
{
	"accessKey":"5E45YvymDy6xUTkkktN3l5eew6hi4ksvOXqog",
	"preserveAccessKeyOnLogout":false,
	"proxy":null,
	"noProxy":false,
	"customServerUrl":"http://192.168.1.28:3000"
}
```
你想要的全都在这了，想重置可以直接删除这个文件，不放心的话可以先做下备份




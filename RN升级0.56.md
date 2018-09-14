<h1><center>如何在升级后的react-native中使用装饰器</center></h1>

1.错误代码：

```
error: bundling failed: TypeError: Property right of AssignmentExpression expected node to be of a type ["Expression"] but instead got null
```

2.原因

新版本rn使用babel@7.0+,所以不能再使用原先的babel-plugin-transform-decorators-legacy(babel@6以下使用)

3.解决方法：

1）

```
	npm install --save-dev @babel/plugin-proposal-decorators
```

2）配置.babelrc

```
{
  "presets": ["react-native"],
  "plugins":[["@babel/plugin-proposal-decorators", { "legacy": true }]]
}
```
3）版本号@babel/plugin-proposal-decorators和在项目的目录下打开yarn.lock文件，即可查看版本号保持一致



4）mobx 版本最新的5.0多报错

	Can't find variable: Symbol 
所以可以用的版本号为：

```
"mobx": "^4.3.1",
"mobx-react": "^5.1.0",
```
5）完整的package.json

```
{
  "name": "DmeoMobx3",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node node_modules/react-native/local-cli/cli.js start",
    "test": "jest"
  },
  "dependencies": {
    "mobx": "^4.3.1",
    "mobx-react": "^5.1.0",
    "react": "16.4.1",
    "react-native": "0.56.0"
  },
  "devDependencies": {
    "@babel/core": "7.0.0-beta.47",
    "@babel/plugin-proposal-decorators": "7.0.0-beta.47",
    "@babel/plugin-transform-runtime": "7.0.0-beta.47",
    "@babel/runtime": "7.0.0-beta.47",
    "babel-jest": "23.4.2",
    "babel-preset-react-native": "^5",
    "jest": "23.5.0",
    "react-test-renderer": "16.4.1"
  },
  "jest": {
    "preset": "react-native"
  }
}

```


原文地址： [https://www.jianshu.com/p/9434957df401](https://www.jianshu.com/p/9434957df401)

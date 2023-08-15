
# 说明
- 来自网友基于 [qwerty472123/wxappUnpacker](https://github.com/qwerty472123/wxappUnpacker "wxappUnpacker") 改进的开源项目。
- 来自网友基于 [xdmjun/wxappUnpacker](https://github.com/xdmjun/wxappUnpacker "wxappUnpacker") 改进的开源项目。
- 本项目仅用于学习研究使用，请勿将本项目的任何内容用于商业或非法目的，否则后果自负。

# 安装
```
npm install
```

# 安装依赖
```
npm install esprima

npm install css-tree

npm install cssbeautify

npm install vm2

npm install uglify-es

npm install js-beautify
```

# 分包功能

当检测到 wxapkg 为子包时, 添加-s 参数指定主包源码路径即可自动将子包的 wxss,wxml,js 解析到主包的对应位置下.

完整流程大致如下:
1. 获取主包和若干子包
2. 解包主包
    - windows系统使用: `./bingo.bat testpkg/master-xxx.wxapkg`
    - Linux系统使用: `./bingo.sh testpkg/master-xxx.wxapkg`
3. 解包子包
    - windows系统使用: `./bingo.bat testpkg/sub-1-xxx.wxapkg -s=../master-xxx`
    - Linux系统使用:  `./bingo.sh testpkg/sub-1-xxx.wxapkg -s=../master-xxx`

觉得麻烦?可以使用[自助解包客户端](#自助解包客户端)

TIP
> -s 参数可为相对路径或绝对路径, 推荐使用绝对路径, 因为相对路径的起点不是当前目录 而是子包解包后的目录

```
├── testpkg
│	├── sub-1-xxx.wxapkg #被解析子包
│	└── sub-1-xxx               #相对路径的起点
│		├── app-service.js
│	├── master-xxx.wxapkg
│	└── master-xxx             # ../master-xxx 就是这个目录
│		├── app.json
```

# 自助解包客户端
mp-unpack.Setup.1.1.1.exe

由于app.json结构有变化, 安装后需要将本项目的 wuConfig.js 覆盖 mp-unpack/resources/tool/wuConfig.js


# 常见错误

Console显示 ``` app.js错误: TypeError: _typeof3 is not a function ```

按错误提示找到文件 ``` @babel/runtime/helpers/typeof.js ```

* 原文内容:
```
function _typeof(o) {
    return "function" == typeof Symbol && "symbol" == typeof Symbol.iterator ? module.exports = _typeof = function(o) {
        return typeof o;
    } : module.exports = _typeof = function(o) {
        return o && "function" == typeof Symbol && o.constructor === Symbol && o !== Symbol.prototype ? "symbol" : typeof o;
    }, _typeof(o);
}
module.exports = _typeof;
```

* 替换为:
```
function _typeof2(o) {
  "@babel/helpers - typeof";
  return (_typeof2 = "function" == typeof Symbol && "symbol" == typeof Symbol.iterator ? function(o) {
      return typeof o;
  } : function(o) {
      return o && "function" == typeof Symbol && o.constructor === Symbol && o !== Symbol.prototype ? "symbol" : typeof o;
  })(o);
}
function _typeof(o) {
  return "function" == typeof Symbol && "symbol" === _typeof2(Symbol.iterator) ? module.exports = _typeof = function(o) {
      return _typeof2(o);
  } : module.exports = _typeof = function(o) {
      return o && "function" == typeof Symbol && o.constructor === Symbol && o !== Symbol.prototype ? "symbol" : _typeof2(o);
  }, _typeof(o);
}
module.exports = _typeof;
```

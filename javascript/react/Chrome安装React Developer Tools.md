### Chrome (谷歌浏览器) 安装 React Developer Tools 扩展工具包
```
    第一步：下载react-devtools
        # 1.克隆项目
        git clone https://github.com/facebook/react-devtools.git

        # 2.进入 react-devtools 
        cd react-devtools

        # 3.切换分支(v3)
        git checkout v3

        # 4.npm 安装依赖
        npm i
        或者
        npm --registry https://registry.npm.taobao.org install (国内使用淘宝镜像代理)

        # 5.npm 打包扩展程序
        npm run build:extension:chrome

        # 6.查看是否有这个目录
        react-devtools/shells/chrome/build/unpacked
    
    第二步：Chrome 添加扩展程序包
        1、Chrome 导航栏输入
        chrome://extensions/

        2、选择开发者模式
        点击加载已解压的扩展程序，选择路径 react-devtools/shells/chrome/build/unpacked

        3、启动项目并启动React Developer Tools扩展工具


```
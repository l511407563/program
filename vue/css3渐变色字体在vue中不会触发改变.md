####  css3渐变色字体在vue中不会触发改变
```
  vue中使用-webkit-background-clip: text; 和 background-image: linear-gradient 生成的渐变色字体
  如果使用正常的{{ text }} 去生成字体，text改变的时候 页面不会触发变化
  使用 v-html="text", 解决这个bug
  
```

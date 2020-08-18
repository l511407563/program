####  scoped导致v-html样式失效

```
vue 的 <style lang="scss" scoped>  scoped会为样式加上 data-v-5d658f9a 属性，
	会导致改组件中使用 v-html生成的元素样式失效
解决办法：
	1. 删除scoped
	2. 直接在元素上写style
```

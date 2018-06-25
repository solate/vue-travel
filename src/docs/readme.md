

# 一个旅游网站例子

移动端网页

## 分析

1. 路由: 路由就是根据网址的不同，返回不同的内容给用户

### 多页应用和单页应用

1. 多页应用 ： 页面跳转 => 返回html

* 优点: 首屏时间快，SEO效果好
* 缺点: 页面切换慢

2. 单页应用 ： 页面跳转 => js渲染

* 优点: 页面切换快
* 缺点: 首屏时间稍慢，SEO差


### 初始化

1. 完善index.html, meta name="viewport" 添加

```
minimum-scale=1.0,maximum-scale=1.0,user-scalable=no
```

移动端用户使用手指放大缩小无效

### 移动端1像素边框问题

多像素屏中1像素边框会显示成多像素

1. reset.css 初始化css
2. border.css 一像素解决css


### 移动端300毫秒点击延迟问题

某些浏览器点击click 时间会延迟300毫秒

解决：

```
npm install fastclick --save
```

### iconfont

注册，创建项目，下载图标

```
import './assets/styles/iconfont.css'
```


### stylus

```
npm install stylus --save

npm install stylus-loader --save
```


### rem 布局

移动端一般使用rem进行布局

1rem = html  font-size = 50px

两个元素之间间距大于1个像素, 解决

```
margin-left: -.04rem
```

### css中引入其他css

1. 使用 @import, 不能直接使用import
2. 相对src路径, 使用 `~@` 不能直接 @

```
@import '~@/assets/styles/varibles.styl'
```

#### 在配置中创建路径别名

build/webpack.base.conf.js 文件中 resolve 选项添加

```
resolve: {
  extensions: ['.js', '.vue', '.json'],
  alias: {
    'vue$': 'vue/dist/vue.esm.js',
    '@': resolve('src'),
    'styles': resolve('src/assets/styles'), //起别名
  }
},
```

### 轮播图

使用第三方插件

[轮播图](https://github.com/surmon-china/vue-awesome-swiper)



#### 图片宽高比例自适应

设置height是0, overflow是hidden, padding-bottom:的值是width/height 图片宽度除以高度

```
.wrapper
    overflow: hidden
    width: 100%
    height: 0
    padding-bottom: 31.25%
```

第二种, 可能部分浏览器有问题，所以用上面那种

```
.wrapper
    height: 31.25vw
```


#### 组件css样式穿透

当组件使用scoped, 内部再写的样式就不能改变外部元素的显示，使用 `>>>` 进行穿透

```
.wrapper >>> .swiper-pagination-bullet-active
    background: #fff
```


#### axios 使用


```
npm install axios --save
```


#### better-scroll 使用

isScroll 的封装

城市 字母滚动使用该插件进行滚动

```
npm install better-scroll --save
```



### Vuex

```
npm install vuex --save
```


### localStorage

使用localStorage 本地存储，类似cookie

最好在外部包裹一个 try ... catch 不然有些浏览器关闭的话会抛出异常


### keep-alive

当路由加载过一次后，就将页面放入内存中，下一次不需要渲染页面。

```
<template>
  <div id="app">
    <keep-alive exclude="Detail">
      <router-view/>
    </keep-alive>
  </div>
</template>
```


处理缓存不会每次发送ajax 请求

1. exclude 参数, 除了什么组件不缓存，其他的都缓存
2. activated() 生命周期判断参数是否相同，如果相同不发送，不相同重新发送

```
activated () {
  if (this.lastCity !== this.city) {
    this.lastCity = this.city
    this.getHomeInfo()
  }
}
```

### 滚动行为

scrollBehavior 每次页面切换 x,y 都是0, 也就是顶部

```
scrollBehavior (to, from, savedPosition) {
  return { x: 0, y: 0 }
}
```










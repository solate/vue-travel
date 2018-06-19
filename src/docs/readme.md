

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











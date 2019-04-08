# 基于Vue 2.x的 <垂直循环滚动跑马灯> 组件

<p align="center">
<a href="https://www.npmjs.com/package/vue-rating-it"><img src="https://img.shields.io/npm/v/vue-roll-up.svg?style=flat-square" /></a>
<p>

预览

[在线demo](https://codepen.io/vicco/pen/xBQVJx)

## 功能:
- 支持通过slot自定义显示的内容（增加点击事件等）
- 可自定宽度，行高
- 可自定义字体颜色和背景色
- 可自定义滚动延迟时间
- 可自定义滚动动效速度

## 使用:
通过 npm 指令安装:
> npm i vue-roll-up --save

在组件中加载:
```javascript
 import VueRollUp from 'vue-roll-up'
```

注册组件:
```javascript
component: {
  VueRollUp
}
```

接着，在模版文件中定义组件
```html
<vue-roll-up 
  :roll-list="list"
  :width="300"
  :height="65"
  :color="#FF0000"
  :duration="35000"
  :speed="500"
></vue-roll-up>
```

## 文档:

### 属性
| 属性 | 描述 |  类型 | 默认值 |
| -- | -- | -- | -- |
| roll-list | 需要滚动的数据，数组类型 | Array | - |
| use-slot | 设置为true的话可以在模板中使用slot特性 | Boolean | false |
| width | 配置滚动的整体宽度 | Any | 200 |
| height | 配置滚动的高度和行高 | Any | 35 |
| color | 设置字体颜色 | String | '#333' |
| bg-color | 设置背景色 | String | - |
| duration | 设置滚动延迟时间(millisecond) | Number | 2000 |
| speed | 设置动效速度(millisecond) | Number | 1000 |

### 通过slot给marquee绑定点击事件:

```html
<vue-roll-up :roll-list="list" :width="300">
  <template v-slot="{ marquee }">
    <span @click="doSth">{{ marquee }}</span>
  </template>
</vue-roll-up>
```

> 如发现有任何bug或文档错误请及时联系作者，3Q

## 作者相关
[<如是我闻> - 记录包括设计，前端，后端的个人博客](https://daxian.work/)

[泡面的个人博客](https://vicco.blog)

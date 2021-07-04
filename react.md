[react](http://www.zhufengpeixun.com/grow/html/106.1.react.html#t64.3%20JSX%E8%A1%A8%E8%BE%BE%E5%BC%8F)

### jsx

```js
import React from 'react';
import ReactDOM from 'react-dom';
let element = <h1>hello</h1>
// element  不可扩展，不可修改
// 所谓的渲染，就是按照react元素所描述的结构，创建真实的dom，并将其插入到root容器内
ReactDOM.render(
    element, document.getElementById('root')
)
```

element编译后的结果为

```js
{
  "type": "h1",
  "key": null,
  "ref": null,
  "props": {
    "children": "hello"
  },
  "_owner": null,
  "_store": {}
}
```

所谓的虚拟dom，其实就是一个普通的js对象

- type:元素类型
- key: 用来区分同一个父亲的不同儿子，dom-diff会用到
- ref: 用来获取真实的dom元素
- props: 属性

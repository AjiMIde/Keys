## ios平台（及少数Android）在`input`输入时页面滚动Bug（或Fixed布局时出现滚动问题等）

* 问题描述：在ios页面上，当元素过多时，使用`input`输入时，会出现诸如**页面无法滚动**、**input输入后页面滚动异常**、**Modal弹窗input输入后页面错乱**等等问题
* 或是在**Modal弹窗上滚动时，弹窗后面的页面也跟着滚动的Bug**、**底部input输入时，小键盘遮住input框**等问题
* 解决方法：通过控制页面的不滚动，来解决这样一些问题

#### input输入时，被小键盘遮挡的问题

```js
// 应当在页面渲染完成之后再来设置事件
// 注意，只能使用for循环来遍历Elements
// offsetTop的计算可以根据需求来定，offsetTop/offsetHeight/clientHeight/scollTop等参数的含义需要理解

this.$nextTick(() => {
  const inputs = document.getElementsByTagName('input')
  for (let i = 0; i < inputs.length; i++) {
    inputs[i].onfocus = () => {
      console.log(inputs[i])
      let offsetTop = inputs[i].offsetTop - 50
      document.documentElement.scrollTop = offsetTop
      // 或 
      window.scrollTo(0, offsetTop)
    }
  }
})
```

#### input输入后，解决ios页面无法滚动的问题

```js
// 与上面的解决方案一致的是，同样是使用页面滚动的办法
// 在inpu

this.$nextTick(() => {
  const inputs = document.getElementsByTagName('input')
  for (let i = 0; i < inputs.length; i++) {

      ele.onblur = function () {
        window.setTimeout(() => {
          const scrollHeight = document.documentElement.scrollTop || document.body.scrollTop || 0
          window.scrollTo(0, Math.max(scrollHeight - 1, 0))
        }, 100)
      }
   }
})

```

#### input输入后，解决ios页面布局错乱，滚动错乱的问题

```js
// 实现原理就是设置 document.body.position = 'fixed', 并设置top，
// 当解除时，再把这些样式解开
this.scrollTop = document.scrollingElement.scrollTop
window.document.body.style.top = -this.scrollTop + 'px'
window.document.body.style.position = 'fixed'

// 解除
window.document.body.style.top = 0 + 'px'
window.document.body.style.position = 'relative'
document.scrollingElement.scrollTop = this.scrollTop
```



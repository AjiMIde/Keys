## NProgress.js-顶部激光进度条

* 地址：https://github.com/rstacruz/nprogress

 
#### 顶部激光进度条开发

```bash
# npm install --save nprogress
```

```vue
<script>
import NProgress from 'nprogress/nprogress'
import 'nprogress/nprogress.css'

NProgress.start()
NProgress.done()

</script>
```

* 通常来讲，搭配一些`ajax`进度或路由切换来使用会比较符合日常习惯一点，比如：
* `beforeRouteEnter`与`mounted()->$nextTick()`
* `ajax.start()`与`ajax.done()`

#### 其他命令：

```js
NProgress.set(0.3)
NProgress.inc(0.2)     // incrementing 增加
NProgress.done(true)   // force done
NProgress.configure({
  template: "<div class='....'>...</div>"
})
NProgress.configure({ parent: '#container' });  // 指定在某个位置
```




## axios

* `axios`是基于`promise`的`http`客户端发起工具（支持浏览器及`node.js`）
* 支持`promise API`
* 支持`request``response`拦截

 
#### 安装使用

```bash
npm i axios
```

```js
import axios from 'axios'

// get请求
axios.get(url).then(res => {}).catch(err=>{}).then(alwaysExecuted => {})

// get 方法的url加参也可以写成：
axios.get(url, { params: {a: 'b'}})

// post 请求
axios.post(url, {
  a: 'aa', b: 'bb'
}).then().catch().then()

// 使用 axios 方法发起 get 
axios({
  method: 'get',
  url: 'http://127.0.0.1:7890/',
  params: {
    a: 'aa'
  }
}).then(res => console.log(res))

// 使用 axios 方法发起 post
axios({
  method: 'post',
  url: 'http://127.0.0.1:7890/',
  data: {
    a: 'aa'
  }
}).then(res => console.log(res))
```

#### axios.all()使用

```js
function getA () {
  return axios.get(urlA)
}

function getB () {
  return axios.get(urlB)
}

axios.all([getA(), getB()]).then(axios.spread((acct, perms) => {
  // both request are all complete
  // 一次解决多个并发的请求，并联合处理参数
  // 其中，acct是getA的成功回调
  // 其中，perms是getB的成功回调
}))
```



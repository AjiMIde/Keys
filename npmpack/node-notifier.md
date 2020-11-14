## node-notifier

> * https://www.npmjs.com/package/node-notifier
> * 通过使用 `node.js` 跨平台地发送通知信息。在 `macOS`上为通知中心
> * 在 Linux 上为`notify-osd/libnotify-bin`，在 win8/10上为`Toaster`。

#### 基本使用

```js
const notifier = require('node-notifier');

// Object
notifier.notify({
  title: 'My notification',
  message: 'Hello, there!',
  icon: '' // 须绝对路径
})
```

#### 全量参数
```js
const notifier = require('node-notifier');

// Object
notifier.notify({
  title: 'My notification',
  message: 'Hello, there!',
  icon: '',
  sound: true, // 可以为string，音效路径
  wait: true, // 等待响应，直 action callback
  id: void 0, // Number 用以关闭toaster
  appID: void 0, // String ?
  remove: void 0, // Number ?
  install: void 0, // String 路径、应用程序 app id
  
  time: 5000,     // Number 显示时间 （似乎只在 balloon 上使用）
  type: 'info',   // info/warn/error 只有 balloon 上使用
}, (err, resp) => { // 回调，一般为 click 回调
  console.log(err, resp)
});
notifier.on('click', function(notifierObject, options) {
  // Triggers if `wait: true` and user clicks notification
  console.log('on click', notifierObject, options)
});
notifier.on('timeout', function(notifierObject, options) {
  // Triggers if `wait: true` and notification closes
  console.log('on timeout', notifierObject, options)
});
```

#### 按需引入（只举例 windows toaster/Balloon）

```js
const WindowsToaster = require('node-notifier/notifiers/toaster');
const WindowsBalloon = require('node-notifier/notifiers/balloon');

const configOptions = {
}
const options = {
  title: 'My notification',
  message: 'Hello, there!',
  icon: '',
  sound: true, // Only Notification Center or Windows Toasters，
  wait: false, // Wait with callback, until
}
new WindowsToaster(configOptions).notify(options);
new WindowsBalloon(configOptions).notify(options);  // 气球提醒，在这个方法下面 icon 配置无效
```

#### 注意事项

* win8: 图片须为 png，不大于 1024*1024px，须小于200kb，须使用绝对路径
* win10 秋季创造者更新：在这个版本下，似乎要指定唯一的 `appID` 才能正确使用 `notifier`
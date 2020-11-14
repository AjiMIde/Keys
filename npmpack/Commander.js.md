## Commander.js

> * Commander.js为commandline程序提供强大的参数解析能力.
> * 下面创建一个库名为`person`的例子
> * 
> * 另外可参考另一库：https://www.npmjs.com/package/minimist
> * [commander github](https://github.com/tj/commander.js)
> * https://segmentfault.com/q/1010000000367285
> * https://www.npmjs.com/browse/depended
> * http://www.ruanyifeng.com/blog/2015/05/command-line-with-node.html

#### 基本使用

```js
const person = require('commander')

// 自定义处理函数
function list (val) {
  return val.split(',')
}

person
  .version('0.0.1')
  // .option('命令, --属性', '描述') 这个选项将会输出一个 person.man 为 true/false，当指定了 -m ，则 person.man = true
  .option('-m, --man', 'Add the sex')

  // 这里的属性为 --no-woman，并不是指 person.no-woman，而是 person.woman，当指定了 -w，则 person.woman = false
  .option('-w, --no-woman', 'Add the sex')

  // 指定了 <描述>，则这个属性为必填输入，不填则会影响其他命令的选项输入
  .option('-n, --name <string>', 'A string name')

  // 指定了 [描述]，则这个属性为可选输入，不填则会默认为 person.province = true
  .option('-p, --province [string]', 'Your province')

  // 指定了 parseInt 为值的处理函数
  .option('-a, --age <number>', 'A int age', parseInt)

  // 自定义指定了 list 函数为值的处理函数
  .option('-f, --favorite <items>', 'A favorite list', list)

  // 默认值设定 USA
  .option('-c, --country <string>', 'Your country', 'USA')

// 自定义 help
person.on('--help', function(){
  console.log('')
  console.log('Examples:');
  console.log('  -a <number> 指定年龄 ');
  console.log('  -c <string> 指定国家（默认USA）');
});
person.parse(process.argv)

// # node person.js -m -w -n Curry -a 30 -f basketball,spoof,golf -p XiaLuoTe
console.log(person.man, person.woman, person.name, person.age, person.favorite, person.country, person.province, person.argv)
```

```bash
$ node person.js -V  => 0.0.1
$ node person.js -h  => output help
$ node person.js -m -w -n Curry -a 30 -f basketball,spoof,golf -p XiaLuoTe
$ --------------true false Curry 30 [basketball, spoof, golf] USA XiaLuoTe
```

#### 其他

* 正则表达
* command 命令
* 参数 syntax

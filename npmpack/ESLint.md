## ESLint

#### 私人定制的配置

```js
module.exports = {
  rules: {
    // private
    'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    'no-trailing-spaces': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    'no-multi-spaces': process.env.NODE_ENV === 'production' ? 'error' : 'off'
  }
  // ...
}
```

实现表单提交事件的响应，添加`handleSubmit` 如下：

```js
    <form onSubmit={this.handleSubmit} className="comment-form">
        <input ref={value => this.coment=value} type="text" className="input" />
        <button type="submit" className="submit-btn">提交</button>
      </form>
```


定义`handleSubmit`
```js
handleSubmit = (e) => {
  e.preventDefault()//阻止跳转
}
```
由于使用了ES6的胖箭头语法，所以使用中就不需要bind(this)了


`e.preventDefault()`的作用：
>在提交表单的时候，阻止页面跳转

拿到input的value值:
首先添加ref属性
```js
  <input ref={value => this.coment = value}/>
```
ref的意思是“指针”，后面大括号的内容，也就是
```js
  value => this.coment = value
```
是一个胖箭头函数。其中value指代当前input这个节点对应的Object，然后
```js
this.coment = value
```
就是把input对象，赋值给一个成员变量，目的是在class之内可以随处访问。


如果想在handleSubmit函数中拿到用户输入的文本，就

```js
  handleSubmit = () =>{
    console.log(this.comment.value)
  }
```

如何从输入框中拿到字符串的技巧到这里就搞定了，这是简单的一种方式，另外还可以通过"受控组件"取值。


###修改state

render()函数的本性：

>一旦state变render()函数直接被重新执行

所以界面上有两条评论变成三条根本不需要碰HTML，直接操作state就可以了

###清空input
需要在提交结束后清空input的字符串

`handleSubmit`中添加
```js
  this.comment.value=''
```

但是如果表单中的input比较多，下面的方式更适合：
```js
  handleSubmit = () => {
    this.myForm.reset()
  }
  <form ref={value => this.myForm = value}
  ></form>
```

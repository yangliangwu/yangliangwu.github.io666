---
layout: post
title: "form与formdata"
date: 2018-04-03
categories: 前端
---

# 使用FormData和AJAX上传图片

```javascript
uploadAvatar () {
  // 创造一个文件上传的input标签
  let input = document.createElement('input')
  // 设置为file类型，上传文件
  input.type = 'file'
   // 监听事件，当发生改变时执行函数
  input.onchange = () => {
    // 创建一个FormData对象
    let formdata = new FormData()
    // 使用append方法添加数据，append(key, value)
    formdata.append('avatar', input.files[0])
    // 使用AJAX进行post提交数据，使用箭头函数(使this为vue实例)，res为回调函数参数
    axios.post('/users/avatar', formdata).then(res => {
      // res.data为服务器响应数据
      if (res.data.status === true) {
        this.updateAvatar()
      } else {
        alert('图片上传失败：' + res.data.message)
      }
    }).catch(err => { // 捕获异常，err为回调函数参数，类型为Error
      // 可能出现的异常，例如404，502，网络错误等等
      alert(err.message)
    })
  }
  // 触发点击事件
  input.click()
 
}
```

---

# 使用form标签上传图片

```html
<form action="http://localhost:3000/users/avatar" method="POST" enctype="multipart/form-data">
    <input type="file" name="avatar">
    <button type="submit">提交</button>
</form>
```

# 一个简单的点赞功能

我们会从一个简单的点赞功能讲起。 假设现在我们需要实现一个点赞、取消点赞的功能。

如果你对前端稍微有一点了解，你就顺手拈来：

HTML:
```js
<body>
    <div class='wrapper'>
        <button class='like-btn'>
        <span class='like-text'>点赞</span>
        <span>👍</span>
        </button>
    </div>
</body>
```

为了模拟现实当中的实际情况，所以这里特意把这个 button 里面的 HTML 结构搞得稍微复杂一些。有了这个 HTML 结构，现在就给它加入一些 JavaScript 的行为：

```js

  const button = document.querySelector('.like-btn')
  const buttonText = button.querySelector('.like-text')
  let isLiked = false
  button.addEventListener('click', () => {
    isLiked = !isLiked
    if (isLiked) {
      buttonText.innerHTML = '取消'
    } else {
      buttonText.innerHTML = '点赞'
    }
  }, false)
```

功能和实现都很简单，按钮已经可以提供点赞和取消点赞的功能。这时候你的同事跑过来了，说他很喜欢你的按钮，他也想用你写的这个点赞功能。这时候问题就来了，你就会发现这种实现方式很致命：你的同事要把整个 button 和里面的结构复制过去，还有整段 JavaScript 代码也要复制过去。这样的实现方式没有任何可复用性。

结构复用

现在我们来重新编写这个点赞功能，让它具备一定的可复用。这次我们先写一个类，这个类有 render 方法，这个方法里面直接返回一个表示 HTML 结构的字符串：

```js
  class LikeButton {
    render () {
      return `
        <button id='like-btn'>
          <span class='like-text'>赞</span>
          <span>👍</span>
        </button>
      `
    }
  }
```

然后可以用这个类来构建不同的点赞功能的实例，然后把它们插到页面中。
```js
  const wrapper = document.querySelector('.wrapper')
  const likeButton1 = new LikeButton()
  wrapper.innerHTML = likeButton1.render()

  const likeButton2 = new LikeButton()
  wrapper.innerHTML += likeButton2.render()
```

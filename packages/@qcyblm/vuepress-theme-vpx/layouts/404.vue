<template>
  <div class="theme-container">
    <div class="theme-vpx-content">
      <h1>404</h1>

      <blockquote>{{ getMsg() }}</blockquote>

      <RouterLink to="/">
      返回首页。
      </RouterLink>
    </div>
  </div>
</template>

<script>
const msgs = [
  `这里什么都没有。`,
  `我们怎么到这儿来的？`,
  `那是404。`,
  `看起来我们有一些断开的链接。`
]

export default {
  methods: {
    getMsg () {
      return msgs[Math.floor(Math.random() * msgs.length)]
    }
  }
}
</script>

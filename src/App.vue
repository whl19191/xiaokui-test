<template>
  <div id="app">
    <h1>北京小葵公司前端工程师招聘题目说明</h1>
    源代码<a href="https://github.com/dongqs/xiaokui">https://github.com/dongqs/xiaokui</a>
    <ul>
      <li>0.如认为题目过于简单可不做 直接联系我们</li>
      <li>1.请每隔10分钟git-commit一次 这很重要</li>
      <li>2.按照设计图完成前端</li>
      <li>3.建议使用bootstrap或类似前端框架</li>
      <li>4.分component</li>
      <li>5.实现前端搜索</li>
      <li>6.完成后放到github或类似平台上</li>
    </ul>

    <h3>这是设计图</h3>
    <img src="/static/part1.png"></img>
    <img src="/static/part2.png"></img>

    <hr>
    <h3>请在下面这个半成品的基础上继续</h3>
    <hr>

    <template v-if="db">
      <router-view :db="db"></router-view>
    </template>
    <template v-else>
      <h3>Loading</h3>
    </template>
  </div>
</template>

<script>
export default {
  props: ['db']
}
</script>

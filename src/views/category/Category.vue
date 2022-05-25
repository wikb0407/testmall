<template>
  <div class="wrapper" ref="wrapper">
    <ul class="content">
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
      <li>我是内容</li>
    </ul>
  </div>
  
</template>

<script>
import BScroll from 'better-scroll'
export default {
  name: "Category",
  data(){
    return {
      scroll: null
    }
  },
  mounted(){
    this.scroll = new BScroll(this.$refs.wrapper,{
      probeType:3
    })
    this.scroll.on('scroll',)
  }
}
</script>

<style>
  .wrapper {
    height: 150px;
    background-color: red;
  }
</style>
<template>
  <div>
    {{iid}}
    <div>详情页</div>
  </div>
</template>

<script>
export default {
  name: "Detail",
  data() {
    return {
      iid: null
    }
  },
  created() {
    this.iid = this.$route.params.iid
  }
}
</script>

<style>

</style>
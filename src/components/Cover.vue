<template>
  <div class="cover">
    <span class="title">平安经</span>
  </div>
</template>

<script>
export default {
  name: "Cover",
  props: {
    pagenum: Number
  }
};
</script>

<style scoped lang="less">
.cover {
  background-color: #223357;
  width: 80vw;
  height: 120vw;
}
.title {
  writing-mode: vertical-rl;
  font-size: 5vw;
  background-color: #e3cdc0;
  margin: 40vw 0 0 50vw;
  padding: 10vw 2vw;
}
</style>

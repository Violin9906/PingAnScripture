<template>
  <div class="book">
    <Cover />
    <Flyleaf />
    <Page v-for="i in pages" :key="i" :pagenum="i" />
  </div>
</template>

<script>
import Page from "@/components/Page.vue";
import Cover from "@/components/Cover.vue";
import Flyleaf from "@/components/Flyleaf.vue";

export default {
  name: "PingAn",
  props: {},
  data() {
    return {
      pages: 10
    };
  },
  components: {
    Page,
    Cover,
    Flyleaf
  },
  methods: {
    handleScroll() {
      var scrollTop =
        document.documentElement.scrollTop || document.body.scrollTop;
      //变量windowHeight是可视区的高度
      var windowHeight =
        document.documentElement.clientHeight || document.body.clientHeight;
      //变量scrollHeight是滚动条的总高度
      var scrollHeight =
        document.documentElement.scrollHeight || document.body.scrollHeight;
      //滚动条到底部的条件
      if (scrollTop + windowHeight == scrollHeight) {
        //到了这个就可以进行业务逻辑加载后台数据了
        console.log("到了底部");
        this.pages += 10;
      }
    }
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll, true);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
.book {
  height: 60vh;
  width: 80vw;
  display: block;
  margin: 0 auto;
}
</style>

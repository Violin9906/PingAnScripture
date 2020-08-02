<template>
  <div class="page">
    <p class="pagenum">平安经 第{{ pagenumHan }}</p>
    <p v-for="i in 20" :key="i" class="para">
      <a
        :href="'https://zh.wikipedia.org/?curid=' + list.query.random[i - 1].id"
        >{{ list.query.random[i - 1].title }}</a
      >平安
    </p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Page",
  props: {
    pagenum: String
  },
  data() {
    return {
      list: null
    };
  },
  computed: {
    pagenumHan: function() {
      var num = this.pagenum;
      var chnNumChar = [
        "〇",
        "一",
        "二",
        "三",
        "四",
        "五",
        "六",
        "七",
        "八",
        "九"
      ];
      var chnUnitChar = ["", "十", "百", "千", "万", "亿", "万亿", "亿亿"];
      var strIns = "",
        chnStr = "";
      var unitPos = 0;
      var zero = true;
      while (num > 0) {
        var v = num % 10;
        if (v === 0) {
          if (!zero) {
            zero = true;
            chnStr = chnNumChar[v] + chnStr;
          }
        } else {
          zero = false;
          strIns = chnNumChar[v];
          strIns += chnUnitChar[unitPos];
          chnStr = strIns + chnStr;
        }
        unitPos++;
        num = Math.floor(num / 10);
      }
      return chnStr;
    }
  },
  mounted() {
    axios
      .get(
        "https://zh.wikipedia.org/w/api.php?origin=*&format=json&action=query&list=random&rnlimit=20&rnnamespace=0&userlang=zh-cn"
      )
      .then(response => (this.list = response.data));
  }
};
</script>

<style lang="less" scoped>
.page {
  background-color: #e3cdc0;
  width: auto;
  padding: 5px;
}
.para {
  text-align: center;
}
.pagenum {
  text-align: center;
  font-size: 1.5rem;
}
</style>

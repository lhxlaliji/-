<template>
  <div class="contain" v-if="data!=null">
    <a :href="'http://'+data.data.attributes.url" class="i" target="_blank">
      <img :src="'http://localhost:1337'+data.data.attributes.img.data.attributes.url" alt="出错了" class="imge">
    </a>
    <a href="http://juejin.cn" class="i">
      <img src="../assets/images/ad.png" alt="" class="imge2">
    </a>
  </div>
</template>

<script setup>
import { onBeforeMount } from 'vue'


let { data ,refresh} = await useFetch('http://localhost:1337/api/ad?populate=*')
onBeforeMount(() => {
  refresh()
})
</script>

<style lang="less" scoped>
.contain{
  width: (240/60rem);
  margin-bottom: (15/60rem);
  .i{
    display: inline-block;
      .imge{
        display: inline-block;
        width: (240/60rem);
        height: (200/60rem);
        margin-bottom: (15/60rem);
      }
      .imge2{
        width: (241/60rem);
        height: (74/60rem);
      }
  }
}
</style>
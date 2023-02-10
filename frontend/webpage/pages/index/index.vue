<template>
  <div class="containerA" v-if="data!=null">
      <div class="box" v-for="(value) in data.data" :key="value.id">
        <LazyArticleItem :detail="value"></LazyArticleItem>
      </div>
  </div>
</template>

<script setup>
import { onBeforeMount} from 'vue'
let { data,refresh } = await useFetch('http://localhost:1337/api/articles?populate=*')
onBeforeMount(() => {
  refresh()
})
</script>

<style lang="less" scoped>
.containerA {
  .box {
    padding: (20/60rem) (20/60rem) 0px (20/60rem);
    cursor: pointer;

    &:hover {
      background-color: #FAFAFA;
    }
  }

}
</style>
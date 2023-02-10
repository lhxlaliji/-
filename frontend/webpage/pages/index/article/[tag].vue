<template>
  <div class="container" v-if="data!=null">
    <div class="box" v-for="(value) in data.data[0].attributes.articles.data" :key="value.id">
      <LazyArticleItem :detail="value"></LazyArticleItem>
    </div>
  </div>
</template>

<script setup>
import { onBeforeMount} from 'vue'
const tag = useRoute().params.tag
let { data,refresh } = await useFetch(`http://localhost:1337/api/article-tags?filters[tagname][$eq]=${tag}&populate[articles][populate]=*`)

onBeforeMount(() => {
  refresh()
})

</script>

<style lang="less" scoped>
.container {
  .box {
    padding: (20/60rem) (20/60rem) 0px (20/60rem);
    cursor: pointer;

    &:hover {
      background-color: #FAFAFA;
    }
  }

}
</style>
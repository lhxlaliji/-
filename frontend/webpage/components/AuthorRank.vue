<template>
  <div class="contain">
    <div class="head">
      作者榜
    </div>
    <div class="user" v-if="data != null">
      <div class="item" v-for="(value) in data" :key="value.id">
        <div class="name">{{ value.username }}</div>
        <div class="email">{{ value.email }}</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onBeforeMount } from 'vue'
let { data, refresh } = await useFetch('http://localhost:1337/api/users')
onBeforeMount(() => {
  refresh()
})
</script>

<style lang="less" scoped>
.contain {
  background-color: white;

  .head {
    padding-left: (15/60rem);
    line-height: (42/60rem);
    height: (42/60rem);
    font-size: (15/60rem);
    color: black;
    border-bottom: solid rgb(244, 244, 244);
  }

  .user {
    .item {
      cursor: pointer;
      padding: (15/60rem);

      .name {
        font-size: (18/60rem);
        color: black;
      }

      .email {
        font-size: (13/60rem);
        overflow: hidden;
        text-overflow: ellipsis;
      }
    }
  }
}
</style>
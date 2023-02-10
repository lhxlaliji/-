<template>
  <div class="container" v-if="bar!=null">
    <div class="item" v-for="(value) in bar.data" :key="value.id">
      <div class="list">{{ value.attributes.content }}</div>
      <div class="label" v-if="value.attributes.showLabel">{{ value.attributes.labelContent }}</div>
    </div>
    <div class="pull" v-show="flag">
      <div class="logo"></div>
      <div class="box">
        <div class="item2" v-for="(value) in arr " :key="value.id">
          <div class="list2">{{ value.attributes.content }}</div>
          <div class="label" v-if="value.attributes.showLabel">{{ value.attributes.labelContent }}</div>
        </div>
      </div>
    </div>



  </div>

</template>

<script setup>
import { ref, reactive,onMounted,onBeforeMount} from 'vue'
let arr;
let flag = ref(false)
let { data: bar,refresh } = await useFetch('http://127.0.0.1:1337/api/topbars')
onBeforeMount(() => {
  refresh()
})
//控制下拉框的出现
onMounted(() => {
  if (bar.value.data.length > 7) {
    flag = true
    arr = reactive(bar.value.data.splice(7))
  }
})

</script>

<style lang="less" scoped>
@media screen and (max-width: 650px) {
  .label{
    display: none;
  }

}
.container {
  display: flex;
  height: (60/60rem);

  .item {
    display: flex;
    position: relative;
    cursor: pointer;

    .list {
      line-height: (60/60rem);
      margin-left: (30/60rem);
      font-size:(14/60rem);

      &:hover {
        box-shadow: 0px 1px rgb(30, 128, 255);
        color: rgb(113, 119, 124);
      }
    }

    // 上边的小图标
    .label {
      white-space: nowrap;
      position: absolute;
      font-size: (11/60rem);
      text-align: center;
      background-color: red;
      color: white;
      border-radius: 20%;
      left: (45/60rem);
      top: (12/60rem);
      
    }
  }

  //当超出数量后的下拉框
  .pull {
    align-self: center;
    margin-left: (20/60rem);
    position: relative;
    width: (30/60rem);
    height: (30/60rem);
    border-radius: 50%;
    background-color: rgb(30, 128, 255);
    z-index: 99;
    cursor: pointer;

    &:hover .box {
      display: flex;
    }

    // 箭头
    .logo {
      position: absolute;
      left: (4.5/60rem);
      top: (15/60rem);
      width: 0;
      height: 0;
      border-bottom: solid transparent (10/60rem);
      border-left: solid transparent (10/60rem);
      border-right: solid transparent (10/60rem);
      border-top: solid white (10/60rem);
    }

    // 下拉盒
    .box {
      box-shadow: 3px 2px 3px rgba(112, 112, 112, 0.8);
      position: absolute;
      display: none;
      flex-direction: column;
      border: solid silver;
      background-color: white;
      top: (35/60rem);
      text-align: center;

      .item2 {
        position: relative;
        justify-self: stretch;

        .list2 {
          line-height: (60/60rem);
          font-size: (14/60rem);
          white-space: nowrap;
          padding: (13/60rem) (20/60rem);

          &:hover {
            box-shadow: 0px 1px rgb(30, 128, 255);
            color: rgb(113, 119, 124);
          }
        }

        // 上边的小图标
        .label {
          white-space: nowrap;
          position: absolute;
          font-size: (5/60rem);
          text-align: center;
          background-color: red;
          color: white;
          border-radius: 20%;
          left: (55/60rem);
          top: (12/60rem);
        }
      }

    }

  }
}
</style>
<template>
  <div class="container">
    <div class="topBar">
      <div class="w">
        <div class="logo">
          <img src="../assets/images/icon2-removebg-preview (1).png" alt="loading" class="icon" />
          <span class="font">稀土掘金</span>
        </div>

        <TopBar></TopBar>
        <label class="search">
          <input placeholder="探索稀土掘金" type="text" class="s" />
          <img src="../assets/images/search-removebg-preview.png" alt="loading" class="icon-img" />
        </label>

      </div>
    </div>
    <slot></slot>
  </div>
</template>

<script setup>
import { } from 'vue'


</script>

<style lang="less" scoped>
.container {
  .w {
    width: (1392/60rem);
    height: (60/60rem);
    display: flex;
    align-items: center;
    color: rgb(113, 119, 124);
    .logo {
      height: (60/60rem);
      display: flex;
      align-items: center;
      .icon {
        width: (29/60rem);
        height: (22/60rem);
      }
      .font{
        margin-left: (5/60rem);
        font-size: (23/60rem);
        color: black;
      }

    }

    .search {
      display: flex;
      margin-left: (92/60rem);
      justify-content: space-between;
      align-items: center;
      width: (260/60rem);
      height: (34/60rem);
      border: solid rgb(194, 200, 209);
      border-radius: (3/60rem);
      padding: (1/60rem) (2/60rem) (1/60rem) (5/60rem);
      font-size: (12/60rem);
      overflow: hidden;
      .s{
        width: (144/60rem);
      }
      .icon-img {
        border-radius: (1/60rem);
        width: (44/60rem);
        height: (28/60rem);

        &:hover {
          cursor: pointer;
        }
      }

      &:hover {
        border: solid rgb(145, 149, 156);
      }
    }

  }

  .topBar {
    display: flex;
    border-bottom: solid rgb(241, 241, 241) 1px;
    justify-content: center;

  }
}
</style>
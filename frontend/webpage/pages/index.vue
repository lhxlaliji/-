<template>
    <NuxtLayout>
        <div class="container ">
            <ArticleBar></ArticleBar>
            <div class="w">
                <div class="main">
                    <NuxtPage></NuxtPage>
                </div>
                <div class="aside">
                    <Advertise></Advertise>
                    <AuthorRank></AuthorRank>
                </div>
            </div>
        </div>
    </NuxtLayout>

</template>

<script setup>
import { } from 'vue'
</script>

<style  lang="less" scoped>
.container {
    background-color: rgb(244, 245, 245);
    min-height: 100vh;

    .w {
        margin: auto;
        color: rgb(113, 119, 124);
        display: flex;
        justify-content: space-between;
        width: (961/60rem);

        .main {
            width: (700/60rem);
            padding-bottom: (30/60rem);
            background-color: white;
        }

        .aside {

            width: (240/60rem);
            display: flex;
            flex-direction: column;
        }
    }

}
</style>
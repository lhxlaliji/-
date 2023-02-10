<template>
    <div class="container">
        <NuxtLink :to="{ path:`/articlePage/${props.detail.id}`, query: { tag: props.detail.attributes.article_tags.data[0].id } }  " target="blank">
            <div class="author item">
                {{
                    props.detail.attributes.users_permissions_user.data.attributes.username
                }}
            </div>
            <h1 class="title item">{{ props.detail.attributes.Title }}</h1>
            <p class="descript item">{{ props.detail.attributes.description }}</p>
        </NuxtLink>
    </div>
</template>

<script setup>
import { } from 'vue'
let props = defineProps(['detail'])
</script>

<style lang="less" scoped>
.container {
    display: flex;
    flex-direction: column;
    height: (132/60rem);
    border-bottom: solid rgb(229, 230, 235);

    .author {
        color: rgb(78, 89, 105);
        font-size: (14/60rem);
    }

    .title {
        color: rgb(29, 33, 41);
        font-size: (20/60rem);
    }

    .descript {
        color: rgb(134, 144, 156);
        font-size: (15/60rem);
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    .item {
        margin-top: (10/60rem);
    }
}
</style>
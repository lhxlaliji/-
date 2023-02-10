<template>
    <div class="contain">
        <div class="w">
            <div class="nav" v-if="bar!=null">
                <NuxtLink to="/" class="list" exact-active-class="active">综合</NuxtLink>
                <NuxtLink v-for="(value) in bar.data" :to="`/article/${value.attributes.Tagname}`" class="list"
                    :key="value.id" exact-active-class="active">
                    {{ value.attributes.Tagname }}
                </NuxtLink>
                <!-- 超出后下拉框 -->
                <div class="pull" v-show="flag">
                    <div class="logo"></div>
                    <div class="box">
                        <NuxtLink v-for="(value) in arr" :to="`/article/${value.attributes.Tagname}`" class="item2"
                            :key="value.id" exact-active-class="active">
                            {{ value.attributes.Tagname }}
                        </NuxtLink>
                    </div>
                </div>
            </div>
            <div class="manage">
                标签管理
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref,onBeforeMount ,onMounted} from 'vue'
let { data: bar, refresh } = await useFetch('http://127.0.0.1:1337/api/article-tags')
onBeforeMount(() => {
    refresh()
})
// 控制超出后图标的显示
let arr
let flag = ref(false)
onMounted(() => {
    if (bar.value.data.length > 10) {
        flag = true
        arr = reactive(bar.value.data.splice(10))
    }
})
</script>

<style lang="less" scoped>
.active {
    color: rgb(30, 128, 255);
}

.contain {
    display: flex;
    height: (45/60rem);
    justify-content: center;
    border-bottom: solid rgb(241, 241, 241) 1px;
    background-color: white;
    margin-bottom: (15/60rem);
    position: sticky;
    top: 0;

    .w {
        color: rgb(113, 119, 124);
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: (961/60rem);
        font-size: (13/60rem);

        .nav {
            display: flex;

            .list {
                display: inline-block;
                height: (45/60rem);
                line-height: (45/60rem);
                margin-right: (23/60rem);

                &:hover {
                    color: rgb(30, 128, 255);
                }

            }

            //下拉

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
                        line-height: (60/60rem);
                        font-size: 14px;
                        white-space: nowrap;
                        padding: (3/60rem) (20/60rem);

                        &:hover {
                            color: rgb(30, 128, 255);
                        }
                    }

                }

            }
        }

        .manage {
            height: (45/60rem);
            line-height: (45/60rem);

            &:hover {
                color: rgb(30, 128, 255);
                cursor: pointer;
            }
        }
    }

}
</style>
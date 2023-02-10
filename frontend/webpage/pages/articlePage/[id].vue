<template>
    <NuxtLayout>
        <div class="container" v-if="data != null">
            <div class="w">
                <div class="main">
                    <h1>{{ data.data.attributes.Title }}</h1>
                    <div class="markdown-here-wrapper"></div>
                </div>
                <div class="aside">
                    <div class="author">
                        <div class="head">作者</div>
                        <div class="name">
                            {{
                                data.data.attributes.users_permissions_user.data.attributes.username
                            }}
                        </div>
                        <div class="email">
                            {{
                                data.data.attributes.users_permissions_user.data.attributes.email
                            }}
                        </div>
                    </div>
                    <div class="relativeArticle">
                        <div class="head">相关文章</div>
                        <NuxtLink v-for="(value) in relate" :key="value.id"
                            :to="{ path: `/articlePage/${value.id}`, query: { tag: value.attributes.article_tags.data[0].id } }"
                            class="atc" target="blank">
                            <h1 class="title ">{{ value.attributes.Title }}</h1>
                            <p class="descript ">{{ value.attributes.description }}</p>
                        </NuxtLink>
                    </div>
                    <div class="nav">
                        <div class="head">目录</div>
                        <a v-for="(value) in nav" :href="`#${value.id}`" class="a">{{ value.content }}</a>
                    </div>
                </div>
            </div>
        </div>
    </NuxtLayout>
</template>


<script setup>
import { onBeforeMount, onMounted, reactive } from 'vue'
import showdown from 'showdown'
const route = useRoute()//获取路由id
const tag = route.query.tag//文章的标签的id
const articleID = route.params.id//文章的id
let { data, refresh } = await useFetch(`http://localhost:1337/api/articles/${articleID}?populate=*`)
let tags = await useFetch(`http://localhost:1337/api/article-tags/${tag}?populate[articles][populate]=*`)//请求相关文章
let relate  //相关文章的数组
let nav  //用于渲染导航的数组
refresh()
tags.refresh()
onMounted(() => {
    refresh()
    tags.refresh()
    let converter = new showdown.Converter();
    let html = converter.makeHtml(data.value.data.attributes.content)
    document.getElementsByClassName('markdown-here-wrapper')[0].innerHTML = html//将文章内容的md格式转为html，放入容器中


    //过滤出相关文章
    relate = reactive(tags.data.value.data.attributes.articles.data.filter((value) => value.id != articleID))
    console.log(relate);


    //利用正则表达式取出h2里的内容并加入id
    const regH = /<h2 id="([\s\S]*?)">([\s\S]*?)<\/h2>/g
    const regId = /(?<=")(-)*(\d)+/
    const regContent = /(?<=>)[^<]+/

    let label = html.match(regH)
    nav = label.map((item) => {
        let id = item.match(regId)[0]
        let content = item.match(regContent)[0]
        return {
            id: id,
            content: content
        }
    })
    console.log(nav);
})

</script>



<style lang="less" scoped>
.container {
    background-color: rgb(244, 245, 245);
    min-height: 100vh;

    .w {
        margin: auto;
        width: (1140/60rem);
        display: flex;
        justify-content: space-between;
        padding-top: (20/60rem);

        .main {
            width: (820/60rem);
            background-color: white;
            padding: (37/60rem) (32/60rem);

            .markdown-here-wrapper {
                font-size: (18/60rem);
                line-height: 1.8em;
                letter-spacing: 0.1em;

                pre,
                code {
                    font-size: (14/60rem);
                    font-family: Roboto, 'Courier New', Consolas, Inconsolata, Courier, monospace;
                    margin: auto 5px;
                }

                code {
                    white-space: pre-wrap;
                    border-radius: 2px;
                    display: inline;
                }

                pre {
                    font-size: (15/60rem);
                    line-height: 1.4em;
                    display: block;
                }

                pre code {
                    white-space: pre;
                    overflow: auto;
                    border-radius: 3px;
                    padding: 1px 1px;
                    display: block !important;
                }

                strong,
                b {
                    color: #BF360C;
                }

                em,
                i {
                    color: #009688;
                }

                hr {
                    border: 1px solid #BF360C;
                    margin: 1.5em auto;
                }

                p {
                    margin: 1.5em 5px !important;
                }

                table,
                pre,
                dl,
                blockquote,
                q,
                ul,
                ol {
                    margin: 10px 5px;
                }

                ul,
                ol {
                    padding-left: 15px;
                }

                li {
                    margin: 10px;
                }

                li p {
                    margin: 10px 0 !important;
                }

                ul ul,
                ul ol,
                ol ul,
                ol ol {
                    margin: 0;
                    padding-left: 10px;
                }

                ul {
                    list-style-type: circle;
                }

                dl {
                    padding: 0;
                }

                dl dt {
                    font-size: 1em;
                    font-weight: bold;
                    font-style: italic;
                }

                dl dd {
                    margin: 0 0 10px;
                    padding: 0 10px;
                }

                blockquote,
                q {
                    border-left: 2px solid #009688;
                    padding: 0 10px;
                    color: #777;
                    quotes: none;
                    margin-left: 1em;
                }

                blockquote::before,
                blockquote::after,
                q::before,
                q::after {
                    content: none;
                }

                h1,
                h2,
                h3,
                h4,
                h5,
                h6 {
                    margin: 20px 0 10px;
                    padding: 0;
                    font-style: bold !important;
                    color: #009688 !important;
                    text-align: center !important;
                    margin: 1.5em 5px !important;
                    padding: 0.5em 1em !important;
                }

                h1 {
                    font-size: 24px !important;
                    border-bottom: 1px solid #ddd !important;
                }

                h2 {
                    font-size: 20px !important;
                    border-bottom: 1px solid #eee !important;
                }

                h3 {
                    font-size: 18px;
                }

                h4 {
                    font-size: 16px;
                }


                table {
                    padding: 0;
                    border-collapse: collapse;
                    border-spacing: 0;
                    font-size: 1em;
                    font: inherit;
                    border: 0;
                    margin: 0 auto;
                }

                tbody {
                    margin: 0;
                    padding: 0;
                    border: 0;
                }

                table tr {
                    border: 0;
                    border-top: 1px solid #CCC;
                    background-color: white;
                    margin: 0;
                    padding: 0;
                }

                table tr:nth-child(2n) {
                    background-color: #F8F8F8;
                }

                table tr th,
                table tr td {
                    font-size: 16px;
                    border: 1px solid #CCC;
                    margin: 0;
                    padding: 5px 10px;
                }

                table tr th {
                    font-weight: bold;
                    color: #eee;
                    border: 1px solid #009688;
                    background-color: #009688;
                }

            }
        }

        .aside {
            width: (300/60rem);

            .author {
                background-color: white;
                cursor: pointer;
                padding: (15/60rem);
                margin-bottom:(15/60rem);

                .head {
                    line-height: (42/60rem);
                    height: (42/60rem);
                    font-size: (15/60rem);
                    color: black;
                    border-bottom: solid rgb(244, 244, 244);
                    margin-bottom: (20/60rem);
                }

                .name {
                    font-size: (18/60rem);
                    color: black;
                }

                .email {
                    font-size: (15/60rem);
                }
            }

            .relativeArticle {
                background-color: white;
                padding: (15/60rem);
                margin-bottom: (15/60rem);

                .head {
                    line-height: (42/60rem);
                    height: (42/60rem);
                    font-size: (15/60rem);
                    color: black;
                    border-bottom: solid rgb(244, 244, 244);
                    margin-bottom: (20/60rem);
                }

                .atc {
                    color: black;

                    &:hover .title {
                        color: rgb(30, 128, 255);
                    }

                    &:hover .descript {
                        color: rgb(30, 128, 255);
                    }

                    .title {
                        font-size: (20/60rem);
                    }

                    .descript {
                        font-size: (15/60rem);
                        white-space: nowrap;
                        overflow: hidden;
                        text-overflow: ellipsis;
                    }
                }
            }

            .nav {
                background-color: white;
                padding: (15/60rem);
                margin-bottom: (15/60rem);

                .head {
                    line-height: (42/60rem);
                    height: (42/60rem);
                    font-size: (15/60rem);
                    color: black;
                    border-bottom: solid rgb(244, 244, 244);
                    margin-bottom: (20/60rem);
                }

                .a {
                    display: block;
                    padding: (15/60rem);
                    font-size: (15/60rem);
                    margin: (2/60rem);

                    &:hover {
                        background-color: rgb(244, 244, 244);
                    }

                    &:link {
                        box-shadow: -3px 0px rgb(30, 128, 255);
                    }
                }
            }
        }
    }
}
</style>
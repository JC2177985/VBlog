<template>
<div v-title data-title="Team 躬行求真">
    <el-container>

        <el-main class="me-articles">
            <!-- <article-scroll-page>

            </article-scroll-page> -->
            <h1 class="f-title">区块链不等于虚拟加密货币，为何它们相生相伴？</h1>
            <div class="post-time"><span>置顶</span><span>2019-11-20</span><span>来源:科技日报</span></div>
            <div class='f-image'>
                <img src="http://cms-bucket.ws.126.net/2019/11/20/07203e9aa9be4376bdc94beacd504a7f.jpeg" width="100%" />
            </div>
            <div>
                <p>比特币的造富神话带火了一个烧脑的技术——区块链，一个最高价可飙升到19850美元（2017年12月）的虚拟货币自顾自地形成了火热的币圈。更有浑水摸鱼者打着区块链的幌子，写一份白皮书，发行一套代币，再让媒体造势拉盘，交易所里挂几天就能集资千万元。</p>

                <p>2018年以来，各国金融体系对各类代币发行融资活动叫停或抵制，区块链技术随之遇冷。时隔一年，区块链又火了，带火的不止于币圈，还有区块链在各个行业的应用。近日，有媒体报道，区块链热潮下仍存在币圈乱象，叫嚣“双11”可暴富100倍的操作，其实是非法集资。</p>

            </div>
            <div class="f-text">
                <a href="https://tech.163.com/19/1120/11/EUE1JDO1000999LD.html" target="_blank">阅读全文</a>
            </div>
        </el-main>

        <el-aside>
            <card-me class="me-area"></card-me>
            <card-tag :tags="hotTags"></card-tag>
            <card-article cardHeader="最热文章" :articles="hotArticles"></card-article>
            <card-archive cardHeader="文章归档" :archives="archives"></card-archive>
            <card-article cardHeader="最新文章" :articles="newArticles"></card-article>
        </el-aside>

    </el-container>
</div>
</template>

<script>
import ArticleScrollPage from '@/views/common/ArticleScrollPage'
import CardArticle from '@/components/card/CardArticle'
import CardMe from '@/components/card/CardMe'
import CardTag from '@/components/card/CardTag'
import CardArchive from '@/components/card/CardArchive'

import {
    getArticles,
    getHotArtices,
    getNewArtices
} from '@/api/article'
import {
    getHotTags
} from '@/api/tag'
import {
    listArchives
} from '@/api/article'

export default {
    name: 'Index',
    data() {
        return {
            hotTags: [],
            hotArticles: [],
            newArticles: [],
            archives: []
        }
    },
    components: {
        'card-article': CardArticle,
        'card-me': CardMe,
        'card-tag': CardTag,
        ArticleScrollPage,
        CardArchive
    },
    methods: {
        getHotArtices() {
            let that = this
            getHotArtices().then(data => {
                that.hotArticles = data.data
            }).catch(error => {
                if (error !== 'error') {
                    that.$message({
                        type: 'error',
                        message: '最热文章加载失败!',
                        showClose: true
                    })
                }
            })
        },
        getNewArtices() {
            let that = this
            getNewArtices().then(data => {
                that.newArticles = data.data
            }).catch(error => {
                if (error !== 'error') {
                    that.$message({
                        type: 'error',
                        message: '最新文章加载失败!',
                        showClose: true
                    })
                }
            })
        },
        getHotTags() {
            let that = this
            getHotTags().then(data => {
                that.hotTags = data.data
            }).catch(error => {
                if (error !== 'error') {
                    that.$message({
                        type: 'error',
                        message: '最热标签加载失败!',
                        showClose: true
                    })
                }
            })
        },
        listArchives() {
            listArchives().then((data => {
                this.archives = data.data
            })).catch(error => {
                if (error !== 'error') {
                    that.$message({
                        type: 'error',
                        message: '文章归档加载失败!',
                        showClose: true
                    })
                }
            })
        }
    },
    created() {
        // this.getHotArtices()
        // this.getNewArtices()
        // this.getHotTags()
        // this.listArchives()
    }
}
</script>

<style scoped>
.f-text {
    margin: 20px;
    display:flex;
    align-items: center;
}

.f-text a{
    margin-left:auto;

}


p {
    display: block;
    margin-block-start: 1em;
    margin-block-end: 1em;
    margin-inline-start: 0px;
    margin-inline-end: 0px;
    margin: 20px;
    text-indent: 2em;
    /* text-indent 就文章的开头缩进2个空格 */
    }

.f-image {
    margin: 20px;
}

.f-image img {
    height: 300px;
}

.post-time {
    margin-top: 20px;
    font: 12px/1 Arial, Sim sun;
    color: #888;
}

.post-time span {
    margin-left: 20px;
    color: #888;
}

.f-title {
    margin: 20px;
}

.me-articles {
    background: #fff;
    box-shadow: 0 2px 12px 0 rgba(0, 0, 0, .1);
    border: 1px solid #ebeef5;
}

.el-container {
    width: 960px;
}

.el-aside {
    margin-left: 20px;
    width: 260px;
}

.el-main {
    padding: 0px;
    line-height: 16px;
}

.el-card {
    border-radius: 0;
}

.el-card:not(:first-child) {
    margin-top: 20px;
}
</style>

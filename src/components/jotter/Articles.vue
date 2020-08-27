<template>
  <div style="margin-top: 40px">
    <!--<el-button @click="addArticle()">添加文章</el-button>-->
    <div class="articles-area">
      <el-card style="text-align: left">
        <div v-for="article in articles" :key="article.id">
          <div style="float:left;width:85%;height: 150px;">
            <router-link class="article-link" :to="{path:'jotter/article',query:{id: article.id}}"><span style="font-size: 20px"><strong>{{article.article_title}}</strong></span></router-link>
            <el-divider content-position="left">{{article.article_date}}</el-divider>
            <router-link class="article-link" :to="{path:'jotter/article',query:{id: article.id}}"><p>{{article.article_abstract}}</p></router-link>
          </div>
          <el-image
            style="margin:18px 0 0 30px;width:100px;height: 100px"
            :src="article.article_cover"
            fit="cover"></el-image>
          <el-divider></el-divider>
        </div>
      </el-card>
    </div>
    <el-pagination
      background
      layout="total, prev, pager, next, jumper"
      @current-change="handleCurrentChange"
      :page-size="pageSize"
      :total="total">
    </el-pagination>
  </div>
</template>

<script>

export default {
  name: 'Articles',
  data () {
    return {
      articles: [],
      pageSize: 4,
      total: 0
    }
  },
  mounted () {
    this.loadArticles()
  },
  methods: {
    loadArticles () {
      var _this = this
      this.$axios.get('/article/listArticles?page=1&size=' + this.pageSize).then(resp => {
        if (resp && resp.data.status === 0) {
          _this.articles = resp.data.data
          _this.total = resp.data.totalElements
        }
      })
    },
    handleCurrentChange (page) {
      var _this = this
      this.$axios.get('/article/listArticles?page=' + page + '&size='+ this.pageSize).then(resp => {
        if (resp && resp.data.status === 0) {
          _this.articles = resp.data.data
          _this.total = resp.data.totalElements
        }
      })
    }
  }
}
</script>

<style scoped>
  .articles-area {
    width: 990px;
    height: 750px;
    margin-left: auto;
    margin-right: auto;
  }

  .article-link {
    text-decoration: none;
    color: #606266;
  }

  .article-link:hover {
    color: #409EFF;
  }
</style>

<template>
    <el-col :span="3" class="articles-area" style="margin-top: -8px">
      <el-card style="text-align: left">
        <div v-for="article in articles" :key="article.id">
          <div style="float:left;width:85%;height: 150px;">
            <router-link class="article-link" :to="{path:'jotter/article',query:{id: article.id}}">
                <span style="font-size: 20px">
                  <strong>{{article.title}}</strong>
                </span>
            </router-link>
            <el-divider content-position="left">
              <i class="el-icon-edit"></i>
              <span> {{article.publishDate}}</span>
              <i class="el-icon-folder"></i>
              <span> {{article.type}}</span>
            </el-divider>
            <router-link class="article-link" :to="{path:'jotter/article',query:{id: article.id}}">
              <p>{{article.introduction}}</p>
            </router-link>
          </div>
          <el-image
            style="margin:18px 0 0 30px;width:100px;height: 100px"
            :src="article.cover"
            fit="cover"></el-image>
          <el-divider></el-divider>
        </div>
      </el-card>
      <br>
      <el-pagination
        background
        layout="total, prev, pager, next, jumper"
        @current-change="handleCurrentChange"
        :page-size="pageSize"
        :total="3">
      </el-pagination>
    </el-col>
</template>

<script>
  export default {
    name: "ArticlesIndex",
    data() {
      return {
        articles: [],
        pageSize: 2,
        total: 1
      }
    },
    mounted() {
      this.loadArticles()
      this.loadPage()
    },
    methods: {
      loadArticles() {
        var _this = this;
        this.$axios.get('/article/listArticles/1/' + this.pageSize).then(resp => {
          if (resp && resp.data.status === 0) {
            _this.articles = resp.data.data
          }
        })
      },
      loadPage() {
        this.$axios.get('/article/statistics/countArticle').then(resp => {
          if (resp && resp.data.status === 0) {
            var articlesNum = resp.data.data;
            this.total =  Math.ceil(articlesNum / this.pageSize);
            console.info(this.total)
          }
        })
      },
      handleCurrentChange(page) {
        var _this = this;
        this.$axios.get('/article/listArticles/' + page + '/' + this.pageSize).then(resp => {
          if (resp && resp.data.status === 0) {
            _this.articles = resp.data.data
          }
        })
      }
    }
  }
</script>

<style scoped>

  .articles-title {
    width: 200px;
  }
  .articles-area {
    width: 1000px;
  }
  .article-link {
    text-decoration: none;
    color: #606266;
  }

  .article-link:hover {
    color: #409EFF;
  }
</style>

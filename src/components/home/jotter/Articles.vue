<template>
  <div style="height:100%;width:100%">
    <el-row type="flex" justify="center">
      <el-col :span="3">
        <el-card class="articles-title" shadow="always">
          <div slot="header" class="clearfix">
            <span>vilce</span>
          </div>
          <div class="el-card__body mid" style="margin-left: -18px">
            <div class="text item" style="text-align: left; margin-top: -18px">
              <i class="el-icon-s-home"></i>
              <span>博客首页</span>
            </div>
            <div class="text item" style="text-align: left">
              <i class="el-icon-menu"></i>
              <span>分类</span>
            </div>
            <div class="text item" style="text-align: left">
              <i class="el-icon-s-order"></i>
              <span>归档</span>
            </div>
            <div class="text item" style="text-align: left; margin-bottom: -18px">
              <i class="el-icon-search"></i>
              <span>搜索</span>
            </div>
          </div>
        </el-card>
      </el-col>
      <el-col :span="3" class="articles-area">
        <el-card style="text-align: left">
          <div v-for="article in articles" :key="article.id">
            <div style="float:left;width:85%;height: 150px;">
              <router-link class="article-link" :to="{path:'jotter/article',query:{id: article.id}}">
                <span style="font-size: 20px">
                  <strong>{{article.title}}</strong>
                </span>
              </router-link>
              <el-divider content-position="left">{{article.date}}</el-divider>
              <router-link class="article-link" :to="{path:'jotter/article',query:{id: article.id}}">
                <p>{{article.introduction}}</p>
              </router-link>
            </div>
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
    </el-row>
  </div>
</template>

<script>
  export default {
    name: 'Articles',
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
        this.$axios.get('/article/countArticle').then(resp => {
          if (resp && resp.data.status === 0) {
            var articlesNum = resp.data.data;
            this.total =  Math.ceil(articlesNum / this.pageSize);
            console.info(this.total)
          }
        })
      },
      handleCurrentChange(page) {
        var _this = this;
        this.$axios.get('/article/countArticle/' + page + '/' + this.pageSize).then(resp => {
          if (resp && resp.data.status === 0) {
            _this.articles = resp.data.data
          }
        })
      }
    }
  }
</script>

<style>
  .text {
    font-size: 14px;
  }

  .item {
    margin-bottom: 10px;
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }

  .clearfix:after {
    clear: both
  }

  .articles-title {
    width: 200px;
  }

  .articles-area {
    width: 1000px;
  }

  .el-card__header {
    background-color: #1F1F1F;
    font-size: 28px;
    color: #eaeaea;
  }

  .article-link {
    text-decoration: none;
    color: #606266;
  }

  .article-link:hover {
    color: #409EFF;
  }
</style>

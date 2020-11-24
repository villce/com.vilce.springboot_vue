<template>
  <div style="height:100%;width:100%">
    <el-row :gutter="5" type="flex" justify="center">
      <el-col :span="3">
        <el-card class="articles-title" shadow="always">
          <el-row slot="header" class="clearfix" @click.native="backHome">
            <i class="el-icon-s-home"></i>
            <span>vilce</span>
          </el-row>
          <el-row type="flex" justify="center">
            <div class="block">
              <el-avatar :size="70" :src="circleUrl" @click.native="handleAdmin"></el-avatar>
            </div>
          </el-row>
          <el-row class="index" style="text-align: center">
            <el-link>博客<br>{{articleStatistic.articleNum}}</el-link>
            <el-divider direction="vertical"></el-divider>
            <el-link>分类<br>{{articleStatistic.typeNum}}</el-link>
            <el-divider direction="vertical"></el-divider>
            <el-link>标签<br>{{articleStatistic.labelNum}}</el-link>
          </el-row>
        </el-card>
        <br>
        <el-card class="articles-title" shadow="always">
          <div class="el-card__body mid">
            <el-row class="text" style="text-align: left;">
              <el-col v-for="(articleType,i) in articleStatistic.articleTypes" :key="i" :index="(i).toString()"
                      style="text-align: left;padding-bottom: 5px">
                <el-link @click="getArticleByType(articleType.type)">
                  <i class="el-icon-star-on"></i>
                  {{articleType.type}} ({{articleType.num}})
                </el-link>
              </el-col>
            </el-row>
          </div>
        </el-card>
        <br>
        <el-card class="articles-title" shadow="always">
          <div class="el-card__body mid">
            <el-row class="text" style="text-align: left;">
              <el-col id="span_id" v-for="(articleLabel,i) in articleStatistic.articleLabels" :key="i"
                      :index="(i).toString()"
                      style="text-align: left;padding-left: 10px;padding-bottom: 5px">
                <el-link @click="getArticleByLabel(articleLabel.label)" :style="{fontSize: 2*(10-i) +'px'}">
                  {{articleLabel.label}}
                </el-link>
              </el-col>
            </el-row>
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
              <el-divider content-position="left">
                <i class="el-icon-edit"></i>
                <span> {{article.publishDate}}</span>
                <el-divider direction="vertical"></el-divider>
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
          :current-page.sync="currentPage"
          :total="total">
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
        circleUrl: 'https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png',
        articleStatistic: {},
        articles: [],
        pageSize: 2,
        total: 1,
        currentPage: 1
      }
    },
    mounted() {
      this.countArticles();
      this.loadArticles();
    },
    methods: {
      backHome() {
        var _this = this;
        var path = _this.$route.query.redirect
        _this.$router.replace({path: path === '/' || path === undefined ? '/home' : path})
      },
      countArticles() {
        var _this = this;
        this.$axios.get('/article/statistics').then(resp => {
          if (resp && resp.data.status === 0) {
            _this.articleStatistic = resp.data.data;
            this.total = _this.articleStatistic.articleNum;
          }
        })
      },
      loadArticles() {
        var _this = this;
        this.$axios.get('/article/listArticles/1/' + this.pageSize).then(resp => {
          if (resp && resp.data.status === 0) {
            _this.articles = resp.data.data
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
      },
      getArticleByType(type) {
        var _this = this;
        this.$axios.get('/article/getArticleByType/?type=' + type).then(resp => {
          if (resp && resp.data.status === 0) {
            _this.articles = resp.data.data;
            this.total = _this.articles.length;
          }
        })
      },
      getArticleByLabel(label) {
        var _this = this;
        this.$axios.get('/article/getArticleByLabel/?label=' + label).then(resp => {
          if (resp && resp.data.status === 0) {
            _this.articles = resp.data.data;
            this.total = _this.articles.length;
          }
        })
      }
    }
  }
</script>

<style>
  .text {
    font-size: 14px;
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

  .el-card__header {
    background-color: #1F1F1F;
    font-size: 28px;
    color: #eaeaea;
  }

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

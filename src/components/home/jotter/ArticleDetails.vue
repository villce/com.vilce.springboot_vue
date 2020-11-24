<template>
  <div class="articles-area">
    <el-card style="width: 990px;margin: 35px auto 0 auto">
      <div>
        <span style="text-align:center;font-size: 20px"><strong>{{article.title}}</strong></span>
        <el-divider content-position="center">
          <i class="el-icon-edit"></i>
          <span> {{article.publishDate}}</span>
          <el-divider direction="vertical"></el-divider>
          <i class="el-icon-folder"></i>
          <span> {{article.type}}</span>
        </el-divider>
        <div class="markdown-body" style="text-align: left">
          <div v-html="article.contentHtml"></div>
        </div>
      </div>
    </el-card>
  </div>
</template>

<script>
  export default {
    name: 'ArticleDetails',
    data() {
      return {
        article: []
      }
    },
    mounted() {
      this.loadArticle()
    },
    methods: {
      loadArticle() {
        var _this = this;
        this.$axios.get('/article/getOneArticle?id=' + this.$route.query.id).then(resp => {
          if (resp && resp.data.status === 0) {
            _this.article = resp.data.data
          }
        })
      }
    }
  }
</script>

<style scoped>
  @import "../../../styles/markdown.css";
</style>

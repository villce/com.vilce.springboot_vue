<template>
  <el-col :span="3" class="articles-type" style="margin-top: -8px">
    <el-card style="text-align: left">
      <el-row>
        <el-col :span="24" style="text-align: center; margin-top: 50px">
          <span style="font-size: 30px; color: #505458">
            <strong>分类</strong>
          </span>
        </el-col>
        <el-col><br></el-col>
        <el-col><br></el-col>
        <el-col :span="24" style="text-align: center">
          <span style="font-size: 15px; color: #505458">
            目前共计 {{typeNum}} 个分类
          </span>
        </el-col>
        <el-col><br></el-col>
        <el-col><br></el-col>
        <el-col :span="24" style="text-align: left">
          <div v-for="articleType in articleTypes">
            <el-link type="info" style="margin-bottom: 10px" @click="getArticleByType(articleType.type)">
              <span style="font-size: 15px; color: #1F1F1F">
                {{articleType.type}} ({{articleType.num}})
              </span>
            </el-link>
          </div>
        </el-col>
      </el-row>
    </el-card>
  </el-col>
</template>

<script>
  import ArticlesIndex from "./ArticlesIndex"
  export default {
    name: "ArticlesType",
    components: {ArticlesIndex},
    data() {
      return {
        articles: [],
        articleTypes: {},
        typeNum: 0
      }
    },
    mounted() {
      this.statisticsTypes();
    },
    methods: {
      statisticsTypes() {
        var _this = this;
        this.$axios.get('/article/statistics/type').then(resp => {
          if (resp && resp.data.status === 0) {
            _this.articleTypes = resp.data.data;
            _this.typeNum = _this.articleTypes.length
          }
        })
      },
      getArticleByType(type) {
        var _this = this;
        this.$axios.get('/article/getArticleByType?type=' + type).then(resp => {
          if (resp && resp.data.status === 0) {
            _this.articles = resp.data.data;
          }
        })
      }
    }
  }
</script>

<style scoped>
  .articles-type {
    width: 1000px;
  }
</style>

<template>
  <div style="height:100%;width:100%">
    <el-row type="flex" justify="center">
      <el-col :span="3" style="margin-top: -8px">
        <el-card class="articles-title" shadow="always">
          <div slot="header" class="clearfix">
            <span>vilce</span>
          </div>
          <div class="el-card__body mid" style="margin-left: -10px">
            <el-row class="text" style="text-align: left; margin-top: -18px" @click.native="articleHome">
              <i class="el-icon-s-home"></i>
              <span>博客首页</span>
            </el-row>
            <el-row class="text" style="text-align: left" @click.native="articleType">
              <i class="el-icon-menu"></i>
              <span>分类</span>
            </el-row>
            <el-row class="text" style="text-align: left" @click.native="articleLabel">
              <i class="el-icon-s-flag"></i>
              <span>标签</span>
            </el-row>
            <el-row class="text" style="text-align: left; margin-bottom: -18px" @click.native="searchArticle">
              <i class="el-icon-search"></i>
              <span>搜索</span>
            </el-row>
          </div>
        </el-card>
      </el-col>
      <component :is="comName" ref="com"></component>
    </el-row>
  </div>
</template>

<script>
  import ArticlesIndex from "./ArticlesIndex"
  import ArticlesType from "./ArticlesType"
  export default {
    name: 'Articles',
    components: {ArticlesIndex, ArticlesType},
    data() {
      return {
        comName: 'ArticlesIndex'
      }
    },
    mounted() {
    },
    methods: {
      articleHome() {
        this.comName='ArticlesIndex';
        this.$refs.com.dialogFormVisible=true;
      },
      articleType() {
        this.comName='ArticlesType';
        this.$refs.com.dialogFormVisible=true;
      },
      articleArchive() {
        console.info("文章归档")
      },
      articleLabel() {
        console.info("文章标签")
      },
      searchArticle() {
        console.info("搜索文章")
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

  .text:hover {
    color: #409EFF;
  }
</style>

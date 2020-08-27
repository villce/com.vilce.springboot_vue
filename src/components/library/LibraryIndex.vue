<template>
  <el-container>
    <el-aside style="width: 200px;margin-top: 20px">
      <switch></switch>
      <SideMenu @indexSelect="listByCategory" ref="sideMenu"></SideMenu>
    </el-aside>
    <el-main>
      <books class="books-area" ref="booksArea"></books>
    </el-main>
  </el-container>
</template>

<script>
import SideMenu from './SideMenu'
import Books from './Books'

export default {
  name: 'AppLibrary',
  components: {Books, SideMenu},
  methods: {
    listByCategory () {
      var _this = this
      var cid = this.$refs.sideMenu.cid
      this.$axios.get('/library/listBooksByCategory?cid=' + cid).then(resp => {
        if (resp && resp.data.status === 0) {
          _this.$refs.booksArea.books = resp.data.data
          _this.$refs.booksArea.currentPage = 1
        }
      })
    }
  }
}
</script>

<style scoped>
  .books-area {
    width: 990px;
    margin-left: auto;
    margin-right: auto;
  }
</style>

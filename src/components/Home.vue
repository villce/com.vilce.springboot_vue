<template>
  <div>
    <nav-menu></nav-menu>
    <router-view/>
  </div>
</template>

<script>
import NavMenu from './common/NavMenu'
export default {
  name: 'Home',
  components: {NavMenu}
}
</script>

<style scoped>
  .nav-menu{
    background: url("https://upload-images.jianshu.io/upload_images/20351380-be9a26aa5e45df47.jpg") no-repeat;
  }
</style>

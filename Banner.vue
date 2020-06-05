<template>
  <el-carousel indicator-position="outside" :interval="3000" height="700px">
    <el-carousel-item v-for="banner in banner_list" :key="banner.name">
        <img :src="banner.image" style="width: 100%" alt="">
    </el-carousel-item>
  </el-carousel>
</template>

<script>
    export default {
        name: "Banner",
        data(){
          return {
              banner_list:[],
          }
        },
        created(){
            this.$axios({
                url:this.$settings.base_url + '/home/banners/',
                method:'get',
            }).then(response => {
                this.banner_list = response.data
            }).catch(error => {
                window.console.log(error)
            })
        }
    }
</script>

<style scoped>

</style>
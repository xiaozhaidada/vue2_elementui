<template>
  <div>
    <el-button type="info" @click="logout">退出</el-button>
  </div>
</template>

<script>
export default {
    name:'Home',
    data(){
        return{

        }
    },
    methods:{
        // 退出功能
        logout(){
            window.sessionStorage.clear()
            this.$router.push('/login')
        }
    }
}
</script>

<style lang="less" scoped>

</style>
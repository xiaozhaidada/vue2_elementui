<template>
    <div class="login">
        <div class="login_box">
            <!-- 头像区域 -->
            <div class="avatar_box">
                <img src="../assets/logo.png" alt="">
            </div>
            <!-- 表单区域 -->
            <el-form label-width="0px" class="login_form" :model="loginForm" :rules="loginFormRules" ref="loginFormRef">
                <!-- 账号 -->
                <el-form-item prop="username">
                    <el-input prefix-icon="el-icon-user" v-model="loginForm.username"></el-input>
                </el-form-item>
                <!-- 密码 -->
                <el-form-item prop="password"> 
                    <el-input prefix-icon="el-icon-lock" v-model="loginForm.password" type="password"></el-input>
                </el-form-item>
                <el-form-item  class="btns">
                    <el-button type="primary" @click="login">登录</el-button>
                    <el-button type="info" @click="reset">重置</el-button>
                </el-form-item>
            </el-form>
        </div>
    </div>
</template>

<script>
export default {
    name:'Login',
    data(){
        return{
            loginForm:{
                username:'',
                password:'',
            },
            loginFormRules:{
                username:[
                    { required: true, message: '请输入账号', trigger: 'blur' },
                ],
                password:[
                    { required: true, message: '请输入密码', trigger: 'blur' },
                ], 
            }
        }
    },
    methods:{
        // 登录功能
        login(){
            this.$refs.loginFormRef.validate((valid) => {
                if(!valid) return
                // 发送请求
                const res = this.$http.post()
                if(res.code == 200){
                    this.$message({ message: '登录成功', type: 'success'})
                    // 把token保存到本地服务器上
                    window.sessionStorage.setItem("token",res.token)
                    // 路由跳转
                    this.$router.push('/home')
                }
                else{
                    this.$message({ message: '登录失败', type: 'error'})
                }
            })
        },
        // 重置功能
        reset(){
            this.$refs.loginFormRef.resetFields()
        }
    }
}
</script>

<style lang="less" scoped>
.login{
    background-color: #2b4b6b;
    height: 100%;
    .login_box{
        width:450px;
        height: 300px;
        background-color: #fff;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        .avatar_box{
            width: 130px;
            height: 130px;
            border-radius: 50%;
            border: 1px solid #eee;
            padding: 10px;
            background-color: #fff;
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
            top: -65px;
            img{
                width: 100%;
                height: 100%;
                border-radius: 50%;
                background-color: #eee;
                
            }
        }
        .login_form{
            position: absolute;
            bottom: 0px;
            width: 100%;
            padding: 0 20px;
            box-sizing: border-box;
            .btns{
                display: flex;
                justify-content: center;
            }
        }

    }
}
</style>


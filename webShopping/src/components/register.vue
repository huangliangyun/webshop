<template>
  <div class="login">
    <div class="login_body">
      <div class="back" style="float:right;">
        <router-link to="/">
          <button type="button" class="btn btn-info">去购物<i style="font-size:20px;margin-left:5px;" class="fa fa-angle-right"></i></button>
        </router-link>
      </div>
      <div class="login_info">
        <h1 style="margin-left:60px;width:50px;height:50px;"><img src="../assets/捞宝3.png"></h1>
        <form class="form-horizontal" role="form">

          <div class="form-group">
            <label class="control-label ">账号</label>
            <input type="text" class="form-control" placeholder="请填写账号"  v-model="username">
          </div>
          <div class="form-group">
            <label class="control-label ">昵称</label>
            <input type="text" class="form-control" placeholder="请填写昵称"  v-model="nickName">
          </div>
          <div class="form-group">
          <label class="control-label ">密码</label>
          <input type="password" class="form-control" placeholder="请填写密码"  v-model="password">
        </div>
          <div class="form-group">
            <label class="control-label ">确认密码</label>
            <input type="password" class="form-control"placeholder="再次输入密码"  v-model="password2">
          </div>
          <div class="form-group">
              <button type="button" class="form-control" style="background: #fd4401;height:40px;color:#fff;font-size:20px;" @click="registerSeller()">提交注册</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
  import qs from "qs"
  export default {
    data(){
      return{
        username:"",
        password:"",
        password2:"",
        nickName:""
      }
    },
    methods:{
      registerSeller(){
        if(this.name===""||this.username===""||this.password===""||this.desc===""||this.phoneNum===""||this.location===""){
          alert("信息不完整")
        }else{
          var data = qs.stringify({
            role:3,
            username:this.username,
            password:this.password,
            nickName: this.nickName
          });
          this.$axios.get('/register?role='+3+'&username='+this.username+'&password='+this.password+'&nickName='+this.nickName).then( (res)=>{
            if(res.data.resultCode===200){
              alert("注册成功!请登录");
              this.$router.push({
               path:'/login'
              })
            }
            else if(res.data.resultCode===100){
            console.log(res);
              alert("账号已存在，请更换");
              window.event.returnValue = false
            }
          })
        }
      }
    }
  }
</script>

<style scoped lang="stylus">
  .login{
    width:100%;
    color:#fff;
    font-size:16px;
  }
  .login_body{
    position:fixed;
    top:0;
    left:0;
    bottom:0;
    right:0;
    background url("../assets/7.png") no-repeat;
    background-size 100%;
  }
  .login_info{
    position:fixed;
    right:100px;
    top:50px;
    width:320px;
    height:450px;
    border-radius 10px;
    background:rgba(232,232,241,0.3);
    padding:0 30px;
  }
</style>

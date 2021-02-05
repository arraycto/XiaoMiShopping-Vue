<template>
  <div class="login">
    <div class="container">
      <a href="/#/index"><img src="/imgs/login-logo.png" alt=""></a>
    </div>
    <div class="wrapper">
      <div class="container">
        <div class="login-form">
          <h3>
            <!--            <span class="checked">帐号登录</span>-->
            <!--            <span class="sep-line">|</span><span>扫码登录</span>-->
          </h3>
          <div class="input">
            <input type="text" placeholder="请输入帐号" v-model="username">
          </div>
          <div class="input">
            <input type="password" placeholder="请输入密码" v-model="password">
          </div>
          <div class="input">
            <input type="text" placeholder="请输入电话" v-model="phone">
          </div>
          <div class="input">
            <input type="text" placeholder="请输入邮箱" v-model="email">
          </div>
          <div class="btn-box">
            <a href="javascript:;" class="btn" @click="register">注册</a>
          </div>
          <div class="tips">
            <div class="sms" @click="login">已注册？返回登录</div>
            <div class="reg"><span></span>忘记密码？</div>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">
      <div class="footer-link">
        <a href="http://www.tongyi.site" target="_blank">统一哥博客</a><span>|</span>
        <a href="http://www.mi.com" target="_blank">小米官网</a>
      </div>
      <p class="copyright">Copyright ©2020 ZTY All Rights Reserved.</p>
    </div>
  </div>
</template>
<script>
import { mapActions } from 'vuex'
export default {
  name: 'login',
  data () {
    return {
      username: '',
      password: '',
      phone: '',
      email: '',
      userId: ''
    }
  },
  methods: {
    ...mapActions(['saveUserName', 'saveCartCount']),
    login () {
      this.$router.push("/register");
    },
    register () {
      this.axios.get("http://localhost:8080/login/getRegister",{
        params:
            {
              'username': this.username,
              'password': this.password,
              'email': this.email,
              'phone': this.phone
            },}
      ).then((res) => {
        console.log(res)
      })

      //   this.axios.get('http://localhost:8080/login/getRegister',{
    //     params:{
    //     username: this.username,
    //     password: this.password,
    //     email: this.email,
    //     phone: this.phone
    //   },
    // }).then(() => {
    //     this.$message.success('注册成功')
    //   })
    }
  }
}
</script>
<style lang="scss">
.login{
  &>.container{
    height:113px;
    img{
      width:auto;
      height:100%;
    }
  }
  .wrapper{
    background:url('/imgs/login-bg2.jpg') no-repeat center;
    .container{
      height:576px;
      .login-form{
        box-sizing: border-box;
        padding-left: 31px;
        padding-right: 31px;
        width:410px;
        height:510px;
        background-color:#ffffff;
        position:absolute;
        bottom:29px;
        right:0;
        h3{
          line-height:23px;
          font-size:24px;
          text-align:center;
          margin:40px auto 49px;
          .checked{
            color:#FF6600;
          }
          .sep-line{
            margin:0 32px;
          }
        }
        .input{
          display:inline-block;
          width:348px;
          height:50px;
          border:1px solid #E5E5E5;
          margin-bottom:20px;
          input{
            width: 100%;
            height: 100%;
            border: none;
            padding: 18px;
          }
        }
        .btn{
          width:100%;
          height:50px;
          line-height:50px;
          margin-top:10px;
          font-size:16px;
        }
        .tips{
          margin-top:14px;
          display:flex;
          justify-content:space-between;
          font-size:14px;
          cursor:pointer;
          .sms{
            color:#FF6600;
          }
          .reg{
            color:#999999;
            span{
              margin:0 7px;
            }
          }
        }
      }
    }
  }
  .footer{
    height:100px;
    padding-top:60px;
    color:#999999;
    font-size:16px;
    text-align:center;
    .footer-link{
      a{
        color:#999999;
        display:inline-block;
      }
      span{
        margin:0 10px;
      }
    }
    .copyright{
      margin-top:13px;
    }
  }
}
</style>

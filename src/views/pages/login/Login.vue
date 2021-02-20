<!-- =========================================================================================
    File Name: Login.vue
    Description: Login Page
    ----------------------------------------------------------------------------------------
    Item Name: Vuexy - Vuejs, HTML & Laravel Admin Dashboard Template
      Author: Pixinvent
    Author URL: http://www.themeforest.net/user/pixinvent
========================================================================================== -->

<template>
  <div
    class="h-screen flex w-full bg-img vx-row no-gutter items-center justify-center"
    id="page-login"
  >
    <div class="vx-col sm:w-1/2 md:w-1/2 lg:w-3/4 xl:w-3/5 sm:m-0 m-4">
    <div class="logo">
      <img src="../../../assets/images/xiyoulogo.png" alt="">
      <span >教学管理信息服务平台</span>
    </div>
      <vx-card>
        <div slot="no-body" class="full-page-bg-color">
          <div class="vx-row no-gutter justify-center items-center">
            <div class="vx-col hidden lg:block lg:w-1/2">
              <img
                src="@/assets/images/pages/login.png"
                alt="login"
                class="mx-auto"
              />
            </div>

            <div class="vx-col sm:w-full md:w-full lg:w-1/2 d-theme-dark-bg">
              <div class="px-8 pt-8 login-tabs-container">
                <div class="flex flex-wrap justify-between mb-3">
                  <div class="vx-card__title mb-4">
                    <h4 class="mb-4 font-bold">用户登录</h4>
                    <p>欢迎回来，请登录你的账户</p>
                  </div>
                  <div class="flex flex-wrap justify-between mb-3">
                    <img src="../../../assets/images/QRcode.gif" class="w-24 h-24" alt="" />
                  </div>
                </div>
                <vs-tabs>
                  <vs-tab label="学生">
                    <login-student></login-student>
                  </vs-tab>

                  <vs-tab label="教师">
                    <login-firebase></login-firebase>
                  </vs-tab>

                  <vs-tab label="管理员">
                    <login-auth0></login-auth0>
                  </vs-tab>
                </vs-tabs>
              </div>
            </div>
          </div>
        </div>
      </vx-card>
       <div class="footer">
      <p>版权所有© Copyright 1999-2020 西安邮电大学　　中国·西安长安区    版本V-1.0.0</p>
    </div>
    </div>
   
  </div>
</template>

<script>
import LoginFirebase from './LoginFirebase.vue'
import LoginAuth0 from './LoginAuth0.vue'
import LoginStudent from './LoginStudent.vue'

export default {
  components: {
    LoginFirebase,
    LoginAuth0,
    LoginStudent
  }
}
</script>

<style lang="scss">
.login-tabs-container {
  min-height: 505px;

  .con-tab {
    padding-bottom: 14px;
  }

  .con-slot-tabs {
    margin-top: 1rem;
  }
}
  .footer {
    text-align: center;
    color: #8099af;
    font: normal 12px/20px microsoft YaHei;
    margin: 15px;   
}
.logo{
  font: normal 24px/45px "microsoft YaHei";
    color: #1069a4;
    padding-bottom: 8px;
    img{
      vertical-align: middle;
      margin-right: 10px;
    }
}
</style>

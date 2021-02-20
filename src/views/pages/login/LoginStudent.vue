<template>
  <div>
    <vs-input
        v-validate="'required|email|min:3'"
        data-vv-validate-on="blur"
        name="studentNumber"
        icon-no-border
        icon="icon icon-user"
        icon-pack="feather"
        label-placeholder="学号"
        v-model="studentNumber"
        class="w-full"/>
    <span class="text-danger text-sm">{{ errors.first('email') }}</span>

    <vs-input
        data-vv-validate-on="blur"
        v-validate="'required|min:6|max:10'"
        type="password"
        name="password"
        icon-no-border
        icon="icon icon-lock"
        icon-pack="feather"
        label-placeholder="密码"
        v-model="password"
        class="w-full mt-6" />
    <span class="text-danger text-sm">{{ errors.first('password') }}</span>

    <div class="flex flex-wrap justify-between my-5">
        <vs-checkbox v-model="checkbox_remember_me" class="mb-3">记住我</vs-checkbox>
        <router-link to="/pages/forgot-password">忘记密码?</router-link>
    </div>
    <div class="flex flex-wrap justify-between mb-3">
      <vs-button  type="border" @click="registerUser">Register</vs-button>
      <vs-button :disabled="!validateForm" @click="LoginStudent">Login</vs-button>
    </div>
    <!-- <vs-divider></vs-divider>
    <div class="alert alert-danger">
      1.初始密码均为身份证号码后六位<br/>
      2.登陆系统后，请维护好邮箱信息，若密码忘记可通过邮箱找回
    </div> -->
  </div>
</template>

<script>
export default {
  data () {
    return {
      studentNumber: 'admin@admin.com',
      password: 'adminadmin',
      checkbox_remember_me: false
    }
  },
  computed: {
    validateForm () {
      return !this.errors.any() && this.studentNumber !== '' && this.password !== ''
    }
  },
  methods: {
    checkLogin () {
      // If user is already logged in notify
      if (this.$store.state.auth.isUserLoggedIn()) {

        // Close animation if passed as payload
        // this.$vs.loading.close()

        this.$vs.notify({
          title: 'Login Attempt',
          text: 'You are already logged in!',
          iconPack: 'feather',
          icon: 'icon-alert-circle',
          color: 'warning'
        })

        return false
      }
      return true
    },
    LoginStudent () {

      if (!this.checkLogin()) return

      // Loading
      this.$vs.loading()

      const payload = {
        checkbox_remember_me: this.checkbox_remember_me,
        userDetails: {
          studentNumber: this.studentNumber,
          password: this.password
        }
      }

      this.$store.dispatch('auth/LoginStudent', payload)
        .then(() => { this.$vs.loading.close() })
        .catch(error => {
          this.$vs.loading.close()
          this.$vs.notify({
            title: 'Error',
            text: error.message,
            iconPack: 'feather',
            icon: 'icon-alert-circle',
            color: 'danger'
          })
        })
    },
    registerUser () {
      if (!this.checkLogin()) return
      this.$router.push('/pages/register').catch(() => {})
    }
  }
}

</script>
<style scoped>
.alert-danger{color: #a94442;
    background-color: #f2dede;
    border-color: #ebccd1;
    border-radius: 4px;
    }
    .alert {
    padding: 15px;
    margin-bottom: 20px;
    border: 1px solid transparent;
    border-radius: 4px;}
</style>

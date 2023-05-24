<template>
  <div>
    <login v-if="currentPage === 'login'" @handleLogin="handleLogin" @toRegister="toRegister" />
    <register v-if="currentPage === 'register'" @handleRegister="handleRegister" />
    <home v-if="currentPage === 'home'" @handleLogout="handleLogout" />
  </div>
</template>

<script>
import home from './components/home.vue'
import login from './components/login.vue'
import register from './components/register.vue'
import axios from 'axios'

const baseUrl = 'http://localhost:3000'

export default {
  data() {
    return {
      currentPage: null
    }
  },
  components: {
    login,
    register,
    home
  },
  created() {
    if (localStorage.access_token) {
      this.currentPage = 'home'
    } else {
      this.currentPage = 'login'
    }
  },
  methods: {
    //change page register
    toRegister() {
      this.currentPage = 'register'
    },

    // login
    async handleLogin(dataInput) {
      try {
        const { data } = await axios({
          method: 'post',
          url: `${baseUrl}/users/login`,
          data: dataInput
        })
        localStorage.access_token = data.access_token
        this.currentPage = 'home'
      } catch (error) {
        console.log(error)
      }
    },

    // register
    async handleRegister(dataInput) {
      try {
        const { data } = await axios({
          method: 'post',
          url: `${baseUrl}/users/register`,
          data: dataInput
        })
        this.currentPage = 'login'
      } catch (error) {
        console.log(error)
      }
    },

    //logout
    handleLogout() {
      localStorage.clear()
      this.currentPage = 'login'
    }
  }
}
</script>

<style></style>

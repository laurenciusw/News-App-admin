<template>
  <div>
    <login
      v-if="currentPage === 'login'"
      @handleLogin="handleLogin"
      @toRegister="toRegister"
      @googlelogin="googlelogin"
    />
    <register
      v-if="currentPage === 'register'"
      @handleRegister="handleRegister"
      @toLogin="toLogin"
    />
    <home
      v-if="currentPage === 'home'"
      @handleLogout="handleLogout"
      @handleFetchArticle="handleFetchArticle"
      :articles="articles"
      @handleFetchCategory="handleFetchCategory"
      :categories="categories"
      @handleFetchHistory="handleFetchHistory"
      :histories="histories"
      @handleAddArticle="handleAddArticle"
      ref="home"
      @detailArtcile="detailArtcile"
      :article="article"
      @updateArticle="updateArticle"
      @updateStatus="updateStatus"
    />
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
      currentPage: null,
      articles: [],
      categories: [],
      histories: [],
      article: ''
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

    //change page login
    toLogin() {
      this.currentPage = 'login'
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
    },

    //fetch Article
    async handleFetchArticle() {
      try {
        const { data } = await axios({
          method: 'get',
          url: `${baseUrl}/articles`,
          headers: {
            access_token: localStorage.access_token
          }
        })
        this.articles = data
      } catch (error) {
        console.log(error)
      }
    },

    //fetch Category
    async handleFetchCategory() {
      try {
        const { data } = await axios({
          method: 'get',
          url: `${baseUrl}/categories`,
          headers: {
            access_token: localStorage.access_token
          }
        })
        this.categories = data
      } catch (error) {
        console.log(error)
      }
    },

    //fetch History
    async handleFetchHistory() {
      try {
        const { data } = await axios({
          method: 'get',
          url: `${baseUrl}/histories`
        })
        this.histories = data
      } catch (error) {
        console.log(error)
      }
    },

    // add article
    async handleAddArticle(newArticle) {
      console.log(newArticle)
      try {
        const { data } = await axios({
          method: 'post',
          url: `${baseUrl}/articles`,
          headers: {
            access_token: localStorage.access_token
          },
          data: newArticle
        })
        await this.handleFetchArticle()
        await this.$refs.home.changeSection('article')
      } catch (error) {
        console.log(error)
      }
    },

    //detail Article
    async detailArtcile(id) {
      try {
        const { data } = await axios({
          method: 'get',
          url: `${baseUrl}/articles/${id}`,
          headers: {
            access_token: localStorage.access_token
          }
        })
        console.log(data)
        this.article = data
        this.$refs.home.changeSection('articleForm')
      } catch (error) {
        console.log(error)
      }
    },

    // update article
    async updateArticle(newArticle, id) {
      console.log(id, 'dariapp')
      try {
        const { data } = await axios({
          method: 'put',
          url: `${baseUrl}/articles/${id}`,
          headers: {
            access_token: localStorage.access_token
          },
          data: newArticle
        })
        await this.handleFetchArticle()
        await this.$refs.home.changeSection('article')
      } catch (error) {
        console.log(error)
      }
    },
    // update status
    async updateStatus(id, status) {
      console.log(id, status, 'diapp')
      try {
        const { data } = await axios({
          method: 'patch',
          url: `${baseUrl}/articles/${id}`,
          headers: {
            access_token: localStorage.access_token
          },
          data: { status }
        })
        await this.handleFetchArticle()
        await this.$refs.home.changeSection('article')
      } catch (error) {
        console.log(error)
      }
    },

    //google login
    async googlelogin(res) {
      try {
        const google_token = res.credential
        const { data } = await axios({
          method: 'post',
          url: `${baseUrl}/users/google-login`,
          headers: { google_token }
        })

        localStorage.access_token = data.access_token
        this.currentPage = 'home'
      } catch (error) {}
    }
  }
}
</script>

<style></style>

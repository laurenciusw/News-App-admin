<template>
  <!-- Container -->
  <div class="flex flex-wrap min-h-screen w-full content-center justify-center bg-gray-200 py-10">
    <!-- Login component -->
    <div class="flex shadow-md">
      <!-- Login form -->
      <div
        class="flex flex-wrap content-center justify-center rounded-l-md bg-white"
        style="width: 24rem; height: 32rem"
      >
        <div class="w-72">
          <!-- Heading -->
          <h1 class="text-xl font-semibold">Become a member</h1>
          <small class="text-gray-400">Input your data</small>

          <!-- Form -->
          <form @submit.prevent="doRegister" class="mt-4">
            <div class="mb-3">
              <label class="mb-2 block text-xs font-semibold">Username</label>
              <input
                v-model="dataInput.username"
                type="text"
                placeholder="Enter your email"
                class="block w-full rounded-md border border-gray-300 focus:border-purple-700 focus:outline-none focus:ring-1 focus:ring-purple-700 py-1 px-1.5 text-gray-500"
              />
            </div>

            <div class="mb-3">
              <label class="mb-2 block text-xs font-semibold">Email</label>
              <input
                v-model="dataInput.email"
                type="email"
                placeholder="Enter your email"
                class="block w-full rounded-md border border-gray-300 focus:border-purple-700 focus:outline-none focus:ring-1 focus:ring-purple-700 py-1 px-1.5 text-gray-500"
              />
            </div>

            <div class="mb-3">
              <label class="mb-2 block text-xs font-semibold">Password</label>
              <input
                v-model="dataInput.password"
                type="password"
                placeholder="*****"
                class="block w-full rounded-md border border-gray-300 focus:border-purple-700 focus:outline-none focus:ring-1 focus:ring-purple-700 py-1 px-1.5 text-gray-500"
              />
            </div>

            <div class="mb-3">
              <label class="mb-2 block text-xs font-semibold">Phone Number</label>
              <input
                v-model="dataInput.phoneNumber"
                type="text"
                placeholder="Enter your email"
                class="block w-full rounded-md border border-gray-300 focus:border-purple-700 focus:outline-none focus:ring-1 focus:ring-purple-700 py-1 px-1.5 text-gray-500"
              />
            </div>

            <div class="mb-3">
              <label class="mb-2 block text-xs font-semibold">Address</label>
              <input
                v-model="dataInput.address"
                type="text"
                placeholder="Enter your email"
                class="block w-full rounded-md border border-gray-300 focus:border-purple-700 focus:outline-none focus:ring-1 focus:ring-purple-700 py-1 px-1.5 text-gray-500"
              />
            </div>

            <div class="mb-3">
              <reuseableButton :title="(title = 'SIGN UP')"></reuseableButton>
              <!-- <button
                class="mb-1.5 block w-full text-center text-white bg-purple-700 hover:bg-purple-900 px-2 py-1.5 rounded-md"
              >
                Sign Up
              </button> -->
            </div>
          </form>

          <!-- Footer -->
          <div class="text-center">
            <span class="text-xs text-gray-400 font-semibold">Already have account?</span>
            <a @click.prevent="toLogin" href="#" class="text-xs font-semibold text-purple-700"
              >Sign In</a
            >
          </div>
        </div>
      </div>

      <!-- Login banner -->
      <div
        class="flex flex-wrap content-center justify-center rounded-r-md"
        style="width: 24rem; height: 32rem"
      >
        <img
          class="w-full h-full bg-center bg-no-repeat bg-cover rounded-r-md"
          src="https://i.imgur.com/9l1A4OS.jpeg"
        />
      </div>
    </div>
  </div>
</template>

<script>
import reuseableButton from './reuseableButton.vue'

export default {
  data() {
    return {
      dataInput: {
        username: '',
        email: '',
        password: '',
        phoneNumber: '',
        address: ''
      }
    }
  },
  methods: {
    doRegister() {
      this.$emit('handleRegister', this.dataInput)
    },
    toLogin() {
      this.$emit('toLogin')
    }
  },
  components: {
    reuseableButton
  }
}
</script>

<style></style>

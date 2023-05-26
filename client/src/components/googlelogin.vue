<template>
  <div>
    <div id="buttonDiv"></div>
  </div>
</template>

<script>
export default {
  name: 'googlelogin',
  mounted() {
    google.accounts.id.initialize({
      client_id: '1065731815900-jn2vukqorv39ap5lrecsobnq3a7378ph.apps.googleusercontent.com',
      callback: this.googlelogin
    })
    google.accounts.id.renderButton(document.getElementById('buttonDiv'), {
      theme: 'outline',
      size: 'large'
    })
  },
  methods: {
    googlelogin(data) {
      this.$emit('googlelogin', data)
    }
  }
}
</script>

<style></style>

<template>
  <div class="container">
    <h1>Home page</h1>
    <hr>
    <nuxt-link to="/users">Users</nuxt-link>
    <hr>
    <button @click="goToUsers">Users page</button>
  </div>
</template>

<script>
export default {
  methods: {
    goToUsers() {
      this.$router.push('/users')
    }
  }
}
</script>

<style scoped>
hr{
  margin-top: 2rem;
  margin-bottom: 2rem;
}
</style>

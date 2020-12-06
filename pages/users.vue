<template>
  <div>
    <h1>Users</h1>
    <nuxt-link to="/">home</nuxt-link>
    <hr>
    <ul>
      <li v-for="(user) in users" :key="user.id">{{user.name}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  async asyncData(){
    const resp = await fetch('https://jsonplaceholder.typicode.com/users?_limit=5')
    await new Promise(resolve => setTimeout(()=> resolve(),1000))
    const users = await resp.json()
    return {users}
  },
  data: ()=>({
    users: []
  }),
  async mounted() {

  }
}
</script>

<style scoped>
hr{
  margin-top: 2rem;
  margin-bottom: 2rem;
}
</style>

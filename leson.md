# SSR с Nuxt.js. Быстрый старт.

## List of lessons

[lesson 2](https://www.youtube.com/watch?v=roNZFyla_VA&t=314s)

## Resources

[Nuxt.js docs](https://nuxtjs.org)

## Install nuxt.js

Check npx version:

```bash
npx -v
```

create nuxt project

```bash
npx create-nuxt-app nuxt-youtube
```

select no custom server framework, no PWA, Axios etc, no UI framework, no jest or ava, but universal mode...

🎉  Successfully created project nuxt-youtube

  To get started:

```bash
    cd nuxt-youtube
    npm run dev
```

  To build & start for production:

```bash
    cd nuxt-youtube
    npm run build
    npm run start
```

## Project structure

[lesson 3](https://www.youtube.com/watch?v=f2EkBTojVdw)

### Folders

- nuxt &mdash; contains app work files;
- assets &mdash; uncompiled assets
- components
- layouts &mdash; higher level components
- middleware &mdash; contains functions that invoked before render
- pages &mdash; contains app pages
- pligins
- static &mdash; contains static files, like favicon
- store &mdash; this folder is for vuex

### Files

- *package.json* &mdash; as usual;
- nuxt.config.js:
  - mode: universal, means SSR mode.
  - head: content of head section of document.

## Running app in SPA mode

when running app in universal mode, SSR produces code on server side, while changing mode to spa will produce empty html.

## Start working

### Removing Logo component

remove `Logo` component:

```bash
rm components/Logo.vue
```

in `pages/index.vue`  remove Logo component.

```vue
<template>
  <div class="container">
    <h1>Home page</h1>
    <hr>
    <a href="/users">Users</a>
  </div>
</template>

<script>
export default {}
</script>

<style>

</style>

```

### Add style to layout

Update `layout/default.vue`

```vue
<template>
  <div class="default-layout">
    <Nuxt />
  </div>
</template>

<style>
.default-layout{
  padding-top: 5rem;
  padding-left: 5rem;
  padding-right: 5rem;
}
```

If we click link, we'll get 404 error.

## Customize 404 layout

```bash
touch layouts/error.vue
```

## Routing

here is no any router page. Route is based on files. So, for /users route:

```bash
touch pages/users.vue
```

```vue
<template>
  <div>
    <h1>Users</h1>
    <a href="/">home</a>
  </div>
</template>
```

### Nuxt-link

replace a element with:

```vue
<nuxt-link to="/">home</nuxt-link>
```

This prevents page reloading.

## Users page

[lesson 5](https://www.youtube.com/watch?v=2nP-FEUpInM)

[time 4:00](https://www.youtube.com/watch?v=2nP-FEUpInM*t=240s)

use this link to get users json:

https://jsonplaceholder.typicode.com/users

update `users`

```vue
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
  data: ()=>({
    users: []
  }),
  async mounted() {
    const resp = await fetch('https://jsonplaceholder.typicode.com/users?_limit=5')
    this.users = await resp.json()
  }
}
</script>

<style scoped>
hr{
  margin-top: 2rem;
  margin-bottom: 2rem;
}
</style>

```

users are rendered on client side. But nuxt implements asyncData method, which works on server side

```js
async asyncData(){
  console.log('asyncData')
  const resp = await fetch('https://jsonplaceholder.typicode.com/users?_limit=5')
  const users = await resp.json()
  return {users}
},
```

this methods forces list rendering on server side.

## Loading progress bar

This bar is activated by default, just change its color in `nuxt.config.js`:

```js
loading: { color: 'blue', height: '10px'}
}
```


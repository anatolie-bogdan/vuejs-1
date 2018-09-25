<template>
  <div>
    <span class="mr-3">Home page</span>

    <router-link 
      to="/add" 
      class="mr-3">
      Add User
    </router-link>
    <router-link to="/users">
      Open User List
    </router-link>
  </div>
</template>

<script>
export default {
  name: 'IndexPage'
}
</script>

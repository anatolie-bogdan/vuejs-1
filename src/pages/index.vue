<template>
  <div>
    <span class="mr-3">Стартовая страница</span>

    <router-link 
      to="/add" 
      class="mr-3">
      Добавить пользователя
    </router-link>
    <router-link to="/users">
      Открыть список пользователей
    </router-link>
  </div>
</template>

<script>
export default {
  name: 'IndexPage'
}
</script>

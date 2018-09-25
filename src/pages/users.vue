<template>
  <div>
    <h2>Users List</h2>

    <user-list
      title="Total number of users"
      :url="url">
      <tr slot="header">
        <th>#</th>
        <th>First Name</th>
        <th>Last Name</th>
        <th>Active</th>
        <th>Balance</th>
        <th>Email</th>
        <th>Phone</th>
        <th>Registered</th>
      </tr>
      <template
        slot="row"
        slot-scope="props">
        <td>
          <router-link :to="`/edit/${props.id}`"># {{ props.id }}</router-link>
        </td>
        <td>{{ props.firstName }}</td>
        <td>{{ props.lastName }}</td>
        <td>{{ props.isActive }}</td>
        <td>{{ props.balance }}</td>
        <td>{{ props.email }}</td>
        <td>{{ props.phone }}</td>
        <td>{{ props.registered }}</td>
      </template>
    </user-list>

  </div>
</template>

<script>
export default {
  name: 'UsersPage',
  components: {
    'user-list': () => import('@/components/UserList.vue')
  },
  data: () => ({
    // URL загрузки списка пользователей
    url: 'http://localhost:3004/users/'
  })
}
</script>

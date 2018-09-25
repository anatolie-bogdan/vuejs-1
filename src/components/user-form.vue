<!-- Компонент формы пользователя (для редактирования, добавления) -->

<template>
  <div>

    <div
      class="form-group"
      :class="{ 'has-error': errors.has('firstName') }">
      <label>Имя</label>
      <input
        type="text"
        class="form-control"
        v-model="localUser.firstName"
        name="firstName"
        v-validate="'required'" >
      <span
        v-show="errors.has('firstName')"
        class="help-block text-danger">
        {{ errors.first('firstName') }}
      </span>
    </div>

    <div
      class="form-group"
      :class="{ 'has-error': errors.has('lastName') }">
      <label>Last Name</label>
      <input
        type="text"
        class="form-control"
        v-model="localUser.lastName"
        name="lastName"
        v-validate="'required'" >
      <span
        v-show="errors.has('lastName')"
        class="help-block text-danger">
        {{ errors.first('lastName') }}
      </span>
    </div>

    <div
      class="form-group"
      :class="{ 'has-error': errors.has('email') }">
      <label>Email</label>
      <input
        type="text"
        class="form-control"
        v-model="localUser.email"
        name="email"
        v-validate="'required|email'" >
      <span
        v-show="errors.has('email')"
        class="help-block text-danger">
        {{ errors.first('email') }}
      </span>
    </div>

    <div class="form-group">
      <label>Image URL</label>
      <avatar-uploader v-model="localUser.picture" />
    </div>

    <div class="form-group">
      <label>Age</label>
      <input
        type="number"
        class="form-control"
        v-model="localUser.age" >
    </div>

    <div class="form-group">
      <label>Active</label>
      <div class="checkbox-inline">
        <input
          type="checkbox"
          v-model="localUser.isActive" > Да
      </div>
    </div>

    <div class="form-group">
      <label>Access level</label>
      <select
        class="form-control"
        v-model="localUser.accessLevel">
        <option
          v-for="item in accessList"
          :key="item">
          {{ item }}
        </option>
      </select>
    </div>

    <div class="form-group">
      <label>Balance</label>
      <input
        type="text"
        class="form-control"
        v-model="localUser.balance" >
    </div>

    <div class="form-group">
      <label>Phone</label>
      <input
        type="text"
        class="form-control"
        v-model="localUser.phone" >
    </div>

    <div class="form-group">
      <label>Address</label>
      <input
        type="text"
        class="form-control"
        v-model="localUser.address" >
    </div>

    <div class="form-group">
      <label>Company name</label>
      <input
        type="text"
        class="form-control"
        v-model="localUser.company" >
    </div>

    <div class="form-group">
      <label>Bio</label>
      <rich-editor v-model="localUser.about" />
    </div>

    <div class="form-group">
      <label>Registration date</label>
      <datepicker v-model="localUser.registered"/>
    </div>

    <hr>

    <pre>{{ localUser }}</pre>

    <slot name="buttons"/>

  </div>
</template>

<script>
// Используемые плагины
import Vue from 'vue'
import VeeValidate from 'vee-validate'

// Подключаем vee-validate
Vue.use(VeeValidate)

export default {
  name: 'UserForm',
  // Прокидываем область видимости родителя для валидации
  inject: ['$validator'],
  components: {
    Datepicker: () => import('@/components/datepicker.vue'),
    AvatarUploader: () => import('@/components/avatar-uploader.vue'),
    RichEditor: () => import('@/components/rich-editor.vue')
  },
  model: {
    prop: 'user'
  },
  props: {
    // Объект с данными пользователя
    user: {
      type: Object,
      required: true
    }
  },
  data: () => ({
    // Локальный изменяемый объект пользователя
    localUser: null,

    accessList: ['guest', 'user', 'admin']
  }),
  watch: {
    // При изменении локального состояния
    // отправляем объект наверх
    localUser: {
      deep: true,
      handler() {
        this.$emit('input', this.localUser)
      }
    }
  },
  created() {
    // Копируем пользователя в локальное состояние
    this.localUser = Object.assign({}, this.user)
  }
}
</script>

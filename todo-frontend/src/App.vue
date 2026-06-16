<template>
  <div class="app">
    <h1>{{ title }}</h1>
    <p>Xin chào, {{ name }}!</p>

    <!-- v-if / v-else -->
    <p v-if="isLoggedIn">✅ Bạn đã đăng nhập</p>
    <p v-else>❌ Chưa đăng nhập</p>

    <!-- v-for -->
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        {{ todo.text }}
      </li>
    </ul>

    <!-- v-on (xử lý sự kiện) -->
    <button @click="toggleLogin">
      {{ isLoggedIn ? 'Đăng xuất' : 'Đăng nhập' }}
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'Todo App',
      name: 'Anh Cường',
      isLoggedIn: false,
      todos: [
        { id: 1, text: 'Học Vue.js' },
        { id: 2, text: 'Học Spring Boot' },
        { id: 3, text: 'Deploy lên Vercel' },
      ]
    }
  },
  methods: {
    toggleLogin() {
      this.isLoggedIn = !this.isLoggedIn
    }
  }
}
</script>

<style>
.app {
  max-width: 600px;
  margin: 40px auto;
  font-family: Arial, sans-serif;
}
button {
  padding: 8px 16px;
  margin-top: 10px;
  cursor: pointer;
}
</style>
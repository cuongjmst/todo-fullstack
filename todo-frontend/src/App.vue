<template>
  <div class="app">
    <h1>📝 Todo App</h1>

    <div class="stats">
      <span>Tổng: {{ totalTodos }}</span>
      <span>✅ Xong: {{ doneTodos }}</span>
      <span>⏳ Còn lại: {{ remainingTodos }}</span>
    </div>

    <div class="input-group">
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        placeholder="Nhập todo mới..."
      />
      <button @click="addTodo">Thêm</button>
    </div>

    <p v-if="warning" class="warning">{{ warning }}</p>

    <!-- Dùng component TodoItem, lặp qua từng todo -->
    <ul>
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @toggle="toggleTodo"
        @delete="removeTodo"
      />
    </ul>

    <p v-if="todos.length === 0" class="empty">Chưa có todo nào!</p>
  </div>
</template>

<script>
// Import component con
import TodoItem from './components/TodoItem.vue'

export default {
  // Đăng ký component để dùng trong template
  components: {
    TodoItem
  },
  data() {
    return {
      newTodo: '',
      warning: '',
      todos: [
        { id: 1, text: 'Học Vue.js', done: false },
        { id: 2, text: 'Học Spring Boot', done: false },
        { id: 3, text: 'Deploy lên Vercel', done: false },
      ]
    }
  },
  computed: {
    totalTodos() {
      return this.todos.length
    },
    doneTodos() {
      return this.todos.filter(t => t.done).length
    },
    remainingTodos() {
      return this.todos.filter(t => !t.done).length
    }
  },
  watch: {
    newTodo(value) {
      if (value.length > 50) {
        this.warning = '⚠️ Todo không được quá 50 ký tự!'
      } else {
        this.warning = ''
      }
    }
  },
  methods: {
    addTodo() {
      if (!this.newTodo.trim()) return
      if (this.newTodo.length > 50) return

      this.todos.push({
        id: Date.now(),
        text: this.newTodo.trim(),
        done: false
      })
      this.newTodo = ''
    },
    // Xử lý event 'toggle' nhận từ TodoItem
    toggleTodo(id) {
      const todo = this.todos.find(t => t.id === id)
      if (todo) todo.done = !todo.done
    },
    // Xử lý event 'delete' nhận từ TodoItem
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    }
  }
}
</script>

<style>
.app { max-width: 600px; margin: 40px auto; font-family: Arial, sans-serif; padding: 0 16px; }
.stats { display: flex; gap: 16px; margin-bottom: 16px; color: #666; font-size: 14px; }
.input-group { display: flex; gap: 8px; margin-bottom: 12px; }
input[type="text"], input:not([type="checkbox"]) { flex: 1; padding: 8px 12px; border: 1px solid #ddd; border-radius: 6px; font-size: 14px; }
button { padding: 8px 16px; background: #42b883; color: white; border: none; border-radius: 6px; cursor: pointer; }
button:hover { background: #33a06f; }
ul { list-style: none; padding: 0; }
.warning { color: #ff4757; font-size: 13px; }
.empty { color: #aaa; text-align: center; margin-top: 20px; }
</style>
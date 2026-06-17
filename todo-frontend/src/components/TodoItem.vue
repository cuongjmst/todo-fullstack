<template>
  <li :class="{ done: todo.done }">
    <input
      type="checkbox"
      :checked="todo.done"
      @change="$emit('toggle', todo.id)"
    />
    <span>{{ todo.text }}</span>
    <button class="del" @click="$emit('delete', todo.id)">🗑</button>
  </li>
</template>

<script>
export default {
  // Props: dữ liệu nhận từ component cha (App.vue)
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  // emits: khai báo rõ các event mà component này sẽ phát ra
  emits: ['toggle', 'delete']
}
</script>

<style scoped>
li {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px;
  border: 1px solid #eee;
  border-radius: 6px;
  margin-bottom: 8px;
}
li.done span {
  text-decoration: line-through;
  color: #aaa;
}
.del {
  background: #ff4757;
  padding: 4px 8px;
  margin-left: auto;
}
.del:hover {
  background: #cc3344;
}
</style>
<template>
  <ul class="todo-list">
    <li
      :class="{ completed: item.isDone }"
      v-for="(item, index) in todoList"
      :key="item.id"
    >
      <div class="view">
        <input class="toggle" type="checkbox" v-model="item.isDone" />
        <label>{{ item.name }}</label>
        <!-- 子传父 -->
        <button class="destroy" @click="$emit('delTodo', index)"></button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'TodoMain',
  props: ['arr', 'isSel'],
  computed: {
    todoList() {
      if (this.isSel === 'yes') {
        return this.arr.filter((item) => item.isDone)
      } else if (this.isSel === 'no') {
        return this.arr.filter((item) => !item.isDone)
      } else {
        return this.arr
      }
    },
  },
}
</script>

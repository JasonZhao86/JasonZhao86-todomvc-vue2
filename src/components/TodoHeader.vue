<template>
  <header class="header">
    <h1>todos</h1>
    <input
      id="toggle-all"
      class="toggle-all"
      type="checkbox"
      v-model="toggleAll"
    />
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      v-model="todoName"
      @keydown.enter="addTodo"
    />
  </header>
</template>

<script>
export default {
  name: 'TodoHeader',
  props: ['arr'],
  data() {
    return {
      todoName: '',
    }
  },
  methods: {
    addTodo() {
      if (!this.todoName.trim()) {
        alert('不能为空')
        return
      }
      this.$emit('addTodo', this.todoName)
      this.todoName = ''
    },
  },
  computed: {
    toggleAll: {
      get() {
        // 如果没有数据, 直接返回false，不要让全选勾选状态
        return this.arr.length !== 0 && this.arr.every((item) => item.isDone)
      },
      set(value) {
        this.$emit('toggleAll', value)
      },
    },
  },
}
</script>

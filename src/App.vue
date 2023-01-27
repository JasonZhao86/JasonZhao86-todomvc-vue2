<template>
  <section class="todoapp">
    <TodoHeader
      :arr="list"
      @addTodo="addTodo"
      @toggleAll="toggleAll"
    ></TodoHeader>
    <!-- 自定义事件，用于子传父 -->
    <TodoMain :arr="list" @delTodo="delTodo" :isSel="isSel"></TodoMain>
    <TodoFooter
      :arr="list"
      :isSel="isSel"
      @changeType="changeType"
      @clearTodo="clearTodo"
    ></TodoFooter>
  </section>
</template>

<script>
import TodoHeader from './components/TodoHeader'
import TodoMain from './components/TodoMain'
import TodoFooter from './components/TodoFooter'
import './styles/base.css'
import './styles/index.css'
export default {
  data() {
    return {
      list: JSON.parse(localStorage.getItem('todomvc')) || [],
      // list: [
      //   { id: 100, name: '吃饭', isDone: true },
      //   { id: 201, name: '睡觉', isDone: false },
      //   { id: 103, name: '打豆豆', isDone: true },
      // ],
      isSel: 'all',
    }
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  methods: {
    delTodo(index) {
      this.list.splice(index, 1)
    },
    addTodo(name) {
      this.list.push({
        id: this.list.length > 0 ? this.list[this.list.length - 1].id + 1 : 100,
        name,
        isDone: false,
      })
    },
    changeType(typeName) {
      this.isSel = typeName
    },
    clearTodo() {
      this.list = this.list.filter((item) => !item.isDone)
    },
    toggleAll(value) {
      this.list = this.list.map((item) => ({ ...item, isDone: value }))
    },
  },
  watch: {
    list: {
      handler(newVal) {
        localStorage.setItem('todomvc', JSON.stringify(newVal))
      },
      deep: true,
    },
  },
}
</script>

<style></style>

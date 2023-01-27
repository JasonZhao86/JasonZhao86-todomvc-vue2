<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong>{{ count }}</strong></span
    >
    <ul class="filters">
      <li v-for="item in choices" :key="item.id">
        <a
          :class="{ selected: item.type === isSel }"
          href="javascript:;"
          @click="$emit('changeType', item.type)"
          >{{ item.name }}</a
        >
      </li>
    </ul>
    <button class="clear-completed" @click="$emit('clearTodo')">
      清除已完成
    </button>
  </footer>
</template>

<script>
export default {
  name: 'TodoFooter',
  props: ['arr', 'isSel'],
  data() {
    return {
      choices: [
        { id: 1, name: '全部', type: 'all' },
        { id: 2, name: '完成', type: 'yes' },
        { id: 3, name: '未完成', type: 'no' },
      ],
    }
  },
  computed: {
    count() {
      return this.arr.length
    },
  },
}
</script>

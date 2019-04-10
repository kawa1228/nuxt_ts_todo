<template>
  <ul>
    <li v-for="(todo, i) in todos" :key="i">
      <input type="checkbox" :checked="todo.done" @change="toggle(todo)" />
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
    </li>
    <li>
      <input placeholder="What needs to be done?" @keyup.enter="addTodo" />
    </li>
  </ul>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
import { mapMutations } from 'vuex'

@Component({
  methods: {
    ...mapMutations({ toggle: 'toggle' })
  }
})
export default class extends Vue {
  private get todos(): Object {
    console.log(this.$store.state.todos.list)
    return this.$store.state.todos.list
  }

  addTodo(e): void {
    this.$store.commit('add', e.target.value)
    e.target.value = ''
  }
}
</script>

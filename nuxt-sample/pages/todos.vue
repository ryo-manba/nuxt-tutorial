<template>
    <div>
        <header><h3>Todo App</h3></header>
        <input v-model="text" placeholder="タスクを追加" @keyup.enter="addTodo">
        <ol>
            <li v-for="todo in todos">
                <input type="checkbox" :checked="todo.done" @change="toggle(todo)">
                <span :class="{ done: todo.done }">{{ todo.text }}</span>
            </li>
        </ol>
</div>

</template>

<script>
import { mapMutations } from 'vuex'

export default {
    computed: {
        todos () {
            return this.$store.state.todos.list
        }
    },
    methods: {
        addTodo(e) {
            this.$store.commit('todos/add', e.target.value)
            this.text = ''

        },
        ...mapMutations({
            toggle: 'todos/toggle'
        })
    }
}
</script>
<style>
div {
    background-color: #f5f5f5f5;
  color: #444;
  font-family: "Poppins", sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  margin: 0;
}
ol {
    list-style-type: none;
    /* border: 2px skyblue dashed; */
    margin-right: 50px;
}
.done {
    text-decoration: line-through;
}
</style>

<template>
  <section class="todoapp">
    <header class="header">
      <h1>Todos</h1>
      <input type="text" class="new-todo" placeholder="Ajouter une tâche" v-model="newTodo" @keyup.enter="addToDo">
    </header>
    <div class="main">
      <ul class="todo-list">
        <li v-bind:key="todo.id" class="todo" v-for="todo in filteredTodos" :class="{completed: todo.completed}">
          <div class="view">
            <input type="checkbox" v-model="todo.completed" class="toggle">
            <label>{{ todo.name }}</label>
          </div>
        </li>
      </ul>
    </div>
    <footer class="footer">
      <span class="todo-count"><strong>{{ remaining }}</strong> tâches à faire</span>
      <ul class="filters">
        <li><a href="#" class="{selected: filter === 'all}" @click.prevent="filter = 'all'">Toutes</a></li>
        <li><a href="#" class="{selected: filter === 'todo'}" @click.prevent="filter = 'todo'">A faire</a></li>
        <li><a href="#" class="{selected: filter === 'done'}" @click.prevent="filter = 'done'">Faites</a></li>
      </ul>
    </footer>
  </section>
</template>

<script>

export default {
  data () {
    return {
      todos: [
        {
          name: 'Tâche de test',
          completed: false
        }
      ],
      newTodo: '',
      filter: 'all'
    }
  },
  methods: {
    addToDo () {
      this.todos.push({
        completed: false,
        name: this.newTodo
      })
      this.newTodo = ''
    }
  },
  computed: {
    remaining () {
      return this.todos.filter(todo => !todo.completed).length
    },
    filteredTodos () {
      if (this.filter === 'todo') {
        return this.todos(todo => !todo.completed)
      } else if (this.filter === 'done') {
        return this.todos.filter(todo => todo.completed)
      }
      return this.todos
    }
  }
}
</script>

<style src="./todos.css"></style>

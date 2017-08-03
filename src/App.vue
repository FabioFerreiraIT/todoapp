<template>

  <!-- <div id="app">
    <h1>Todo POC App</h1>
    <img src="https://media.licdn.com/mpr/mpr/shrink_200_200/AAEAAQAAAAAAAARKAAAAJGE3MTViNGMyLTUxZGMtNGRkMy1hY2U3LTVhMzU5ZTljNWQ5ZQ.png" />
    <div>
      <todo-list
        class="todoCard"
        v-bind:todos="todos">
      </todo-list>
    </div>
  </div> -->

  <div id="app">
    <h1 class="h1"> Vue.js Todo App </h1>
    <div class="app">
      <div class="todoCard">
        <todo-list v-bind:todos="todos"></todo-list>
        <create-todo v-on:create-todo="createTodo"></create-todo>
      </div>
    </div>
  </div>

</template>

<script>
import sweetalert from 'sweetalert'
import TodoList from './components/TodoList'
import CreateTodo from './components/CreateTodo'

export default {
  name: 'app',
  components: {TodoList, CreateTodo},

  // data function avails data to the template
  data () {
    return {
      todos: [
        {
          title: 'Todo A',
          project: 'Project A',
          done: false
        },
        {
          title: 'Todo B',
          project: 'Project B',
          done: true
        },
        {
          title: 'Todo C',
          project: 'Project C',
          done: false
        },
        {
          title: 'Todo D',
          project: 'Project D',
          done: false
        }
      ]
    }
  },
  methods: {
    createTodo (newTodo) {
      this.todos.push(newTodo)
      sweetalert('Success!', 'To-do created!', 'success')
    }
  }
}
</script>

<style>
#app {
  font-family             : Helvetica;
  -webkit-font-smoothing  : antialiased;
  -moz-osx-font-smoothing : grayscale;
  text-align              : center;
  color                   : #FFF;
  background-color        : #1165AE;
}

#app > h1 {
  padding-top: 30px;
}

#app > img {
  width : 100px;
  height: 100px;
}

p {
  color     : white;
  font-size : 20pt;
}

.todoCard {
  margin : auto;
  color  : #1165AE;
  width  : 30%;
}

</style>

<template>
  <div id="app">
    <div class="container">
      <div class="row mb-2">
        <div class="col">
          <div class="input-group mb-2">
            <input v-model="inputText" type="text" class="form-control" placeholder="Enter what you want to do here...">
            <div class="input-group-append">
              <button @click="addTodo" class="btn btn-primary" type="button">
                <i class="fa fa-plus"></i> Add
              </button>
            </div>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <div class="card">
            <div class="card-body">
              <Todo
              v-for="t in todoList"
              :message="t"
              :key="t"
              @removeTodo="removeTodoHandle"
              @editTodo="editTodoHandle"></Todo>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo.vue'

export default {
  name: 'app',
  components: {
    Todo
  },
  data() {
    return {
      todoList: ['Buy KitKat', 'Go to Senna Labs at 2 P.M.', 'Workout at 5 P.M.', 'Give a flower to June'],
      inputText: null,
    }
  },
  methods: {
    removeTodoHandle: function(todo) {
      this.todoList.splice(this.todoList.indexOf(todo), 1)
    },
    editTodoHandle: function(todo, newTodo) {
      this.$set(this.todoList, this.todoList.indexOf(todo), newTodo)
    },
    addTodo: function() {
      this.todoList.unshift(this.inputText)
      this.inputText = null
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

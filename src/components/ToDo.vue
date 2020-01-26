<template>
  <div id="todo-app">
    <h1>{{ msg }}</h1>

    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <form @submit.prevent="addTodo">
            <input v-model="newToDo" class="form-control" type="text" id="NewTodo" name="NewTodo">
            <!-- <button type="submit" class="btn btn-success mt-4 p-3">ADD TODO</button> -->
          </form>

          <button type="button" @click="allDone" class="btn btn-success">All Done</button>

        </div>

        <span>{{ remaining }}</span>

        <div class="col-md-6 mt-4">

          <!-- <ul class="list-group">
            <li class="list-group-item" v-for="todo in todos" v-bind:key="todo">{{ todo.title }}</li>
          </ul> -->

          <div class="form-check" v-for="todo in todos" v-bind:key="todo">
            <input class="form-check-input" v-model="todo.done" type="checkbox">
            <label :class="{ done:todo.done }" @dblclick="editTodo(todo)">{{ todo.title }}</label>

            <input class="edit" type="text"
          v-model="todo.title"
          v-todo-focus="todo == editedTodo"
          @blur="doneEdit(todo)"
          @keyup.enter="doneEdit(todo)"
          @keyup.esc="cancelEdit(todo)">

            <button type="button" @click="removeTodo(todo)" class="btn-sm btn-danger">Del</button>
          </div>

        </div>

      </div>

    </div>

  </div>
</template>

<script type="text/javascript">

export default {
  name:'ToDo',
  // ---
  data() {
    return {
      msg: 'todo',
      newToDo: '',
      todos:[]
    }
  },
  // ---
  methods:{
    addTodo:function(){
      this.todos.push({
        title: this.newToDo,
        done: false
      });
      this.newToDo  = '';
    },
    // ---
    removeTodo(todo){
      const TodoIndex = this.todos.indexOf(todo);
      this.todos.splice(TodoIndex,1);
    },
    // ---
    allDone(){
      this.todos.forEach(todo =>{
        todo.done = true
      });
    },
    editTodo(todo){
      this.beforeEditCache = todo.title
      this.editedTodo = todo
    },

  },
  computed:{
    remaining:function(){
      return this.todos.length
    },
  }
  // ---
}

</script>

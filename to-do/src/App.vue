<template>
  <div id="app">
    <div class="container grid-xs py-2"><img src="@/assets/to-do-logo.png" alt="to-do logo" class="img-responsive to-do-logo">
      <form @submit.prevent="addTodo(todo)">
        <div class="input-group">
          <input v-model="todo.description" class="form-input" type="text" id="input-to-do" placeholder="Ensira a tarefa">
          <button class="btn btn-primary input-group-btn">Enviar</button>
        </div>
      </form>

      <div class="todo-list">
        <todo v-for="t in todos" :key="t.id" :todo="t" @toggle ="toggleTodo" @remove = "removeTodo"/>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo';
export default {
  name: 'App',
  components: { todo: Todo },
  data(){
    return{todos:[], todo:{checked: false}}
  },
  methods: {
    addTodo(todo) {
      todo.id = Date.now();
      this.todos.push(todo);
      this.todo = {checked: false}
    },
    toggleTodo(todo){
      const index = this.todos.findIndex(iten => iten.id === todo.id);
      if(index > -1){
        const checked = !this.todos[index].checked;
        this.$set(this.todos, index, {...this.todos[index], checked})
      }
    },
    removeTodo(todo){
    const index = this.todos.findIndex(iten => iten.id === todo.id);
    if(index > -1){
      this.$delete(this.todos, index);
    }
    }
  },
}
</script>

<style scoped>
  .to-do-logo{
    max-width: 200px;
    margin: 40px auto;
  }

  .todo-list{
    padding-top: 2rem;
  }
  
</style>

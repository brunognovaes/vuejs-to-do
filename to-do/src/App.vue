<template>
  <div id="app" :class="this.darkTheme ?'bg-dark':'bg-light'">
    <div class="form-group float-right">
        <label class="form-switch" @change="switchTheme()">
          <input type="checkbox">
          <i class="form-icon"></i> Dark Mode
        </label>
      </div>
    <div class="container grid-xs py-2"><img src="@/assets/todo-dark.png" alt="to-do logo" class="img-responsive todo-dark">
      <form @submit.prevent="addTodo(todo)">
        <div class="input-group">
          <input v-model="todo.description" class="form-input" :class="this.darkTheme ?'bg-dark':'bg-light'" type="text" id="input-to-do" placeholder="Ensira a tarefa">
          <button class="btn btn-primary input-group-btn" :class="this.darkTheme ?'bg-primary':'bg-dark'">Enviar</button>
        </div>
      </form>
      <div class="todo-list">
        <todo class="todo" v-for="t in todos" :key="t.id" :todo="t" :darkTheme="darkTheme" @toggle ="toggleTodo" @remove = "removeTodo"/>
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
    return{todos:[], todo:{checked: false}, darkTheme: false}
  },
  methods: {
    addTodo(todo) {
      todo.id = Date.now();
      if(todo.description != undefined){
        this.todos.push(todo);
      }
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
    },
    switchTheme(){
      if(!this.darkTheme){
        this.darkTheme = true;
      }else{
        this.darkTheme = false;
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

  .todo{
    word-wrap: break-word;
    margin: 5px ;
  }
  
  #app{
    position: absolute;
    width: 100%;
    height: 100%;
  }
  
</style>

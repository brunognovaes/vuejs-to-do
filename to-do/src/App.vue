<template>
  <div id="app" :class="'bg-'+theme">
    <div class="form-group float-right">
        <label class="form-switch" @change="switchTheme(theme)">
          <input type="checkbox">
          <i class="form-icon"></i> Dark Mode
        </label>
      </div>
    <div class="container grid-xs py-2"><img src="@/assets/todo-dark.png" alt="to-do logo" class="img-responsive todo-dark">
      <form @submit.prevent="addTodo(todo)">
        <div class="input-group">
          <input v-model="todo.description" class="form-input" :class="'bg-'+theme" type="text" id="input-to-do" placeholder="Ensira a tarefa">
          <button class="btn btn-primary input-group-btn" :class="'bg-'+ buttonTheme">Enviar</button>
        </div>
      </form>

      <div class="todo-list">
        <todo class="todo" v-for="t in todos" :key="t.id" :todo="t" :textTheme="textTheme" :tilesTheme="tilesTheme" @toggle ="toggleTodo" @remove = "removeTodo"/>
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
    return{todos:[], todo:{checked: false}, theme:'light', textTheme:'dark', tilesTheme:'gray', buttonTheme:'dark'}
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
      if(this.theme === 'light'){
        this.theme = 'dark';
        this.textTheme = 'light';
        this.tilesTheme = 'primary';
        this.buttonTheme = 'primary';
      }else{
        this.theme = 'light';
        this.textTheme = 'dark';
        this.tilesTheme = 'gray';
        this.buttonTheme = 'dark';
      }
      console.log('sim')
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

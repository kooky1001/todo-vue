<template>
  <div id="app">
    <div class="col-md-6 offset-md-3">
      <h1 class="text-center mb-4">Todo App</h1>
      <input type="text" class="form-control mb-4" v-model="userInput" @keyup.enter="addNewTodo">

      <div style="margin: 100px">
          <h1 id="stopwatch" >
              00:00:00
          </h1>
          <div>
              <button onclick="startClock()">start</button>
              <button onclick="stopClock()">stop</button>
              <button onclick="resetClock()">reset</button>
          </div>
      </div>

      <div class="list-group mb-4">
        <template v-for="todo in activeTodoList" v-bind:key="todo">
        <button class="list-group-item text-left" @click="toggleTodoState(todo)">
          {{ todo.label }}
        </button>
        </template>
      </div>

      <div class="text-right">
        <button class="btn btn-sm" @click="changeCurrentState('active')">할 일</button>
        <button class="btn btn-sm" @click="changeCurrentState('done')">완료</button>
        <button class="btn btn-sm" @click="changeCurrentState('all')">전체</button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      userInput: '',
      todoList: [],
      currentState: 'active'
    }
  },
  computed: {
    activeTodoList(){
      return this.todoList.filter(todo => this.currentState === 'all' || todo.state === this.currentState);
    }
  },
  methods: {
    changeCurrentState(state){
      this.currentState = state;
    },
    addNewTodo() {
      this.todoList.push({
        label: this.userInput,
        state: 'active'
      });
      this.userInput = '';
    },
    toggleTodoState(todo){
      todo.state = todo.state === 'active' ? 'done' : 'active';
    }
  },
  components: {
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

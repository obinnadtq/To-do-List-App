<template>
  <div>
    <input type="text" class="todo-input" v-model="newTodo" @keyup.enter="addTodo" placeholder="Enter your todos">
    <transition-group name="fade" enter-active-class="animated fadeInUp" leave-active-class="animated fadeOutDown">
    <div v-for="todo in todosFiltered" :key="todo.id" class="todo-item">
      <div class="todo-item-left">
        <input type="checkbox" v-model="todo.completed">
        <div>{{todo.title}}</div>
      </div>

    </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: "Activity",
  data() {
    return {
      todos: [],
      newTodo: "",
      idForTodo: 1,
      filter: "all"
    };
  },
  methods: {
    // create function to add todo
    addTodo() {
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false,
        editing: false
      });
      this.newTodo = "";
      this.idForTodo++;
    }
  },
  computed: {
    // create computed property for all , active and completed todos
    todosFiltered() {
      if (this.filter === "all") {
        return this.todos;
      }
      else if(this.filter === "active") {
        return this.todos.filter(todo => !todo.completed)
      }
      else if(this.filter === "completed") {
        return this.todos.filter(todo => todo.completed)
      }
      return this.todos;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";

.todo-input{
  width: 100%;
  font-size: 18px;
  padding: 10px 18px;
  margin-bottom: 16px;
}

.todo-item{
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.todo-item-left{
  display: flex;
  align-items: center;
}
</style>

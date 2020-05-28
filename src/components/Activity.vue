<template>
  <div>
    <input type="text" class="todo-input" v-model="newTodo" @keyup.enter="addTodo" placeholder="Enter your todos">
    <transition-group name="fade" enter-active-class="animated fadeInUp" leave-active-class="animated fadeOutDown">
    <div v-for="todo in todosFiltered" :key="todo.id" class="todo-item">
      <div class="todo-item-left">
        <input type="checkbox" v-model="todo.completed">
        <div v-if="!todo.editing" @dblclick="editTodo(todo)" class="todo-item-label" :class="{completed: todo.completed}">{{todo.title}}</div>
        <input v-else class="todo-item-edit" v-model="todo.title" @keyup.enter="doneEdit(todo)" @keyup.esc="cancelEdit(todo)" v-focus>
      </div>
      <div class="delete-item" @click="removeTodo(index)">
        &times;
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
      filter: "all",
      beforeEditing: ""
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
    },

    removeTodo(index) {
      this.todos.splice(index, 1)
    },

    editTodo(todo) {
      this.beforeEditing = todo.title;
      todo.editing = true;
    },
    doneEdit(todo) {
      if(todo.title.trim() == ""){
        todo.title = this.beforeEditing
      }
      todo.editing = false;
    },
    cancelEdit(todo) {
      todo.title = this.beforeEditing;
      todo.editing = false;
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
  },

  directives: {
    focus: {
      inserted: function(el){
        el.focus()
      }
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

.delete-item {
  cursor: pointer;
}

.todo-item-label {
  padding: 10px;
  margin-left: 12px;
}

.todo-item-edit {
  margin-left: 12px;
}

.completed {
  text-decoration: line-through;
}
</style>

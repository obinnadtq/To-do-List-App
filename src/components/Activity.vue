<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addTask">
        <input type="text" placeholder="Enter your task for today" v-model="task">
      </form>

      <ul>
        <li v-for="(data,index) in tasks" :key="index">{{data}}
          <button @click="removeTask(index)">Delete</button>
        </li>
        
      </ul>
    </div>
    
  </div>
</template>

<script>
export default {
  name: 'Activity',
  data(){
    return{
      task : '',
      tasks: []
    }
  },
  methods:{
    addTask(){
      this.tasks.push(this.task)
      this.task = ''
    },
    removeTask(id){
      this.tasks.splice(id,1)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";

.holder {
    background: #fff;
  }
  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }

   input {
    width: calc(100% - 40px);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #323333;
    color: #687F7F;
  }

</style>

<script setup>
/* */
</script>

<template>
  <div class="card">
    <h2 class="card-header">My Vue Todo</h2>
    <h3 class="card-name">{{toDoListName}}</h3>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <input type="checkbox" name="taskCheck"/>
        <label class="card-task-label" for="taskCheck">{{ task.name }}</label>
        <button v-show="editShow" @click="deleteTask(index)">Delete</button>
        <button v-show="editShow" @click="editTask(index)">Edit</button>
      </li>
    </ul>
    <div class="card-edit" v-show="editShow">
      <input class="card-input" v-model="taskText" type="text" placeholder="Enter task" />
      <button @click="addTask">SUBMIT</button>
    </div>
    <button @click="editShow = !editShow">Edit</button>
  </div>
</template>

<script>
export default {
  props: {
    toDoListName: String
  },
  data() {
    return {
      editShow: false,
      taskText: "UntitledTask",
      editedTask: null,
      tasks: [
        {
          name: "task 1",
        },
        {
          name: "task 2",
        },
      ],
    };
  },
  methods: {
    addTask() {
      if(this.editedTask === null){
        if (this.taskText.length === 0) {
          return;
        } else {
          this.tasks.push({ name: this.taskText });
          this.taskText = "UntitledTask";
        }
      } else  {
        this.tasks[this.editedTask].name = this.taskText;
        this.editedTask = null;
         this.taskText = "UntitledTask";
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.taskText = this.tasks[index].name;
      this.editedTask = index;
    },
  },
};
</script>

<style>
  ul{
    list-style-type: none;
    padding-left: 0;
  }
  .card {
    width: 200px;
    background-color: rgba(68, 0, 255, 0.685);
    padding: 10px;
    color: rgb(219, 247, 255);
    margin: 10px;
  }
  .card-input{
    width: 90%;
  }
  .card-edit > *{
    margin-bottom: 10px;
  }
  .card-task-label{
    margin-right: 10px;
    margin-left: 10px;
  }

  .card-header, 
  .card-name{
    text-align: center;
  }

  .card-header{
    margin-top: 10px;
  }

</style>

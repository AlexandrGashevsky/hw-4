
<template>
  <div class="app-lists">
    <div :key="index" v-for="(name, index) of listNames" class="app-card">
      <ToDoList   :toDoListName="name" />
      <button class="app-delete-list-button" @click="deleteList(index)">Delete</button>
    </div>
   <!-- <input v-model="taskText" type="text" placeholder="Enter task" />
      <button @click="addTask">SUBMIT</button> -->
      <div class="app-add-and-edit">
        <div v-show="editListsShow" class="app-edit-input">
          <input class="app-input" type="text" placeholder="Enter list name" 
            :value="cardName"
  @input="event => cardName = event.target.value"
          />
          <button @click="addTask">SUBMIT</button> 
        </div>
        <button @click="editListsShow = !editListsShow" class="app-btn">+</button>
      </div>
  </div>
</template>

<script>
 import ToDoList from "@/components/ToDoList.vue";
export default {
  components: {
    ToDoList
  },
  data() {
    return {
      cardName: "UntitledToDo",
      editListsShow: false,
      listNames: ["list 1", "list 2", "list 3"]
    }
  },
  methods:{
    addTask() {
        if (this.cardName.length === 0) {
          return;
        } else {
          this.listNames.push(this.cardName);
          this.editListsShow = !this.editListsShow;
          this.cardName = "UntitledToDo";
        }
    },
    deleteList(index) {
      this.listNames.splice(index, 1);
    },
  }
}
</script>

<style>
  .app-lists{
    display: grid;
    grid-template-columns: repeat(5, 240px);
  }
  .app-btn{
    height: 50px;
    width: 50px;
    font-size: 24px;
    font-weight: 900;
    border: solid 1px rgb(61, 61, 61);
    border-radius: 5px;
    margin: 10px 0 0 0px;
  }
  .app-edit-section{
        margin-top: 35px;
  }

  .app-edit-section > input{
    margin-right: 10px;
  }

  .app-add-and-edit {
    margin: 10px 0 0 10px;
  }

  .app-delete-list-button{
    margin-left: 170px;
  }
</style>

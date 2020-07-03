<template>
  <div id="app" class="container">
    <h1>Todo List</h1>
    
    <add-comp v-bind:todoList="todoList"/>

    <list-todo-comp 
      v-bind:todoList="todoList"
      v-on:deleteTodo="deleteTodo"
      v-on:clickUpdateEvent="clickUpdateEvent"
      v-bind:popupUpdate="popupUpdate"
    />

    <update-comp 
      v-bind:todoList="todoList"
      v-bind:index="indexUpdate"
      v-bind:popupUpdate="popupUpdate"
      v-on:UpdateTodoList="UpdateTodoList"
    />
    <b-button variant="success" v-on:click="SaveFile">Save</b-button>
    
  </div>
</template>

<script>
import AddComp from './components/AddComp';
import ListTodoComp from './components/ListTodoComp';
import UpdateComp from './components/UpdateComp';

import json from '../Files/data.json'

export default {
  name: 'app',
  data () {
    return {
      todoList: json,
      todoList1: [
        { id: 100, todo: 'Wake Up' },
        { id: 101, todo: 'Exercise' },
        { id: 102, todo: 'Take Shower' },
        { id: 103, todo: 'Have Breakfast' },
        { id: 104, todo: 'Go to Work' }
      ],
      popupUpdate: false,
      indexUpdate: -1
    }
  },
  components: {
    AddComp,
    ListTodoComp,
    UpdateComp
  },
  methods: {
    deleteTodo(index){
      this.todoList.splice(index, 1);
    },
    clickUpdateEvent(index){
      this.indexUpdate = index;
      this.popupUpdate = true;
    },
    UpdateTodoList(newUpdate){
      let updateIndex = newUpdate.updateIndex;
      let newtodo = newUpdate.newUpdate;
      this.$set(this.todoList, updateIndex, {id: 100 + updateIndex, todo: newtodo})
      this.popupUpdate = false;
    },
    SaveFile() {
    const data = JSON.stringify(this.todoList)
    const blob = new Blob([data], {type: 'text/plain'})
    const e = document.createEvent('MouseEvents'),
    a = document.createElement('a');
    a.download = "test.json";
    a.href = window.URL.createObjectURL(blob);
    a.dataset.downloadurl = ['text/json', a.download, a.href].join(':');
    e.initEvent('click', true, false, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
    a.dispatchEvent(e);
}
  }
}
</script>

<style>
#app1 {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.container{
  text-align: center;
  width: 100%;
  margin: 0 auto;
  padding: 10px;
  overflow: none;
}

</style>

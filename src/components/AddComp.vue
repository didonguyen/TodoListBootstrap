<template>
  <div class="add-new">
    <h4>Add a new todo</h4>
    <input v-model="todo" type="text" placeholder="Do Something..." id="add-new">
    <b-button variant="success" v-on:click="handleAddNew" class="add-button">Add</b-button>
    </div>
</template>

<script>
export default {
  name: 'AddComp',
  props: {
      todoList: { type:Array, default: [] }
  },
  data() {
      return {
          todo: ''
      }
  },
  methods: {
      handleAddNew(){

          let objTodo = { key: 100 + this.todoList.length, todo: this.todo}
          this.todoList.push(objTodo);
      }
  }
};
</script>

<style>



.add-new{
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: left;
    align-items: center;
    } 
.add-button{
    margin-top: 15px;
}
.add-new input{
    height: 30px;
    flex-grow: 1;
    margin: 0px 15px;
    padding: 0 5px;
    font-size: 18px;
}
@media (min-width: 1200px){
    .add-new{
    height: 100px;
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: left;
    align-items: center;
    }
    .add-button{
    margin-bottom: 15px;
}
}
</style>

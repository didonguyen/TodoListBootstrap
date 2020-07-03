<template>
      <div class="grid container">
          <div class="item" 
            v-for="(item, index) in todoList"
            v-bind:key="index">
              <b-card
                    title=""
                    img-src="https://picsum.photos/600/300/?image=25"
                    img-alt="Image"
                    img-top
                    tag="article"
                    style="max-width: 20rem; margin-right: 10px"
                    class="mb-2"
                    
                >
                <b-card-text>
                {{ item.todo }}
                </b-card-text>

                <b-button variant="primary" v-on:click="handleClickUpdate(index)">Update</b-button>
                <b-button variant="danger" v-on:click="$emit('deleteTodo', index)">Delete</b-button>
                </b-card>
          </div>
        </div>
</template>

<script>
import TodoComp from './TodoComp';
export default {
  name: 'ListTodoComp',
  props: {
      popupUpdate: { type: Boolean, default: false}
  },
  data () {
      return {
          
      }
  },
  props: {
      todoList: { type: Array, default: [] }
  },
  components: {
      TodoComp
  },
  computed: {
      
  },
  methods: {
      handleClickUpdate(index){
        this.$emit('clickUpdateEvent', index);
      }
  }

};
</script>

<style>
    .grid{
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    }

@media (min-width: 1200px){
    .grid{
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    }
}
</style>

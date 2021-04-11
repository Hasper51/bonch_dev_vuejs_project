<template>
    <div>
        <todoitem
            v-for="(todo,i) of todos" 
            :id='i'
            v-bind:todo="todo"
            @remove-todo="removeTodo"
            @edit-todo="editTodo"
        />
         
    </div>    
</template>

<script>
import todoitem from '@/components/todoitem'
export default {
  props: ['todos'],
  components: {
      todoitem
  },
  methods:{
      removeTodo(id){
          this.$emit('remove-todo',id)
      },
      editTodo(id){
          this.$emit('edit-todo',id)
      }
  }

}
</script>

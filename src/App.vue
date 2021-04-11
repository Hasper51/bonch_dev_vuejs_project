<template>
  <div id="app">
    <v-app>
    
      <h3>Итоговый баланс: {{Balance}}</h3>
      <addTodo 
        @add-todo='addTodo'
      />
      <todolist 
        :todos="todos"
        @remove-todo="removeTodo"
        @edit-todo="editTodo"
      />
    </v-app>  
  </div>
</template>

<script>
import todolist from '@/components/todolist'
import addTodo from '@/components/addTodo'
export default {
  name: 'app',
  components: {
    todolist,
    addTodo
  },
  data () {
    return {
      Balance: 0,
      todos: [
        {idd: 1, title: 'Монитор', sum: 5000 , date: '11.04.2021, 16:25:34', type: 'Доход', description: 'Новый'},
        {idd: 2, title: 'Мышь', sum: 2000 , date: '11.04.2021, 16:25:34', type: 'Доход', description: 'Новый'},
        {idd: 3, title: 'Клава', sum: 1500 , date: '11.04.2021, 16:25:34', type: 'Доход', description: 'Новый'}
      ]
    }
  },
  methods: {
    balance(){
      this.Balance = 0
      this.todos.forEach(element => {
        
        if (element.type === "Доход")
          this.Balance+= Number.parseInt(element.sum)
        else if  (element.type === "Расход")
          this.Balance-= Number.parseInt(element.sum) 
      });
    },
    removeTodo(id) {
      this.todos.splice(id,1)
      this.balance()
    },
    addTodo(todo) {
      this.todos.push(todo)
      this.balance()
    },
    editTodo(id,editedtodo){
      this.todos.splice(id,1,editedtodo)
      this.balance()
    }
  }
}
</script>

<style lang="scss">

</style>

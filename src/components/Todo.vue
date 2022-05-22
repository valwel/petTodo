<template>
  <div class="main">
    <div class="header">Введите новую задачу:</div>
    <input v-model="newTodoText" @keypress.enter="onAddTodo" type="text">
    <div class="header">Ваши задачи:</div>
    <ul class="todo">
      <li v-for="item in todoList" :key="item.id" @click="onToggleDone(item)">
        <button @click="deleteTodo(item)">Удалить</button>
        <s v-if="item.isDone">{{item.title}}</s>
        <span v-else>{{item.title}}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'AppTodo',
  data() {
    return {
      newTodoText: '',
      todoList: []
    }
  },

  methods: {
    onToggleDone(item){
      item.isDone = !item.isDone
    },
    onAddTodo(){
      this.todoList.push({
        id: this.todoList.length,
        title: this.newTodoText,
        isDone: false
      }),
      this.newTodoText = ''
    },
    deleteTodo(item){
      this.todoList = this.todoList.filter(currentItem => item.id !== currentItem.id)
    }
  }
}
</script>

<style scoped>
.todo{
  font-size: 32px;
  list-style-type: none;
}

.header{
  font-size: 24px;
  font-weight: bolder;
  text-align: center;
  margin: 20px;
}

button{
  margin-right: 10px;
}
</style>
<template>
  <div class="wrapper">
    <h1>قائمة مهام</h1>
    <div>
      <form class="inputField" @submit.prevent="create">
        <input v-model="newTodo" autocomplete="off">
        <button>إضافة</button>
      </form>
    </div>
    <ul class="todoList">
      <li v-for="item in todos" :key="item.id">
        <h3 :class="{ done : item.completed}" @click="completed(item)">{{item.content}}</h3>
        <button @click="remove(item)">حذف</button>

      </li>
    </ul>
    <div class="footer">
      <button @click="markAll">تحديد الكل</button>
      <button @click="removeAll">حذف الكل</button>
    </div>
  </div>
</template>

<script>
import {ref} from 'vue'

  export default {
    setup () {
      const todos = ref ([])
      const newTodo = ref ('')

      function create () {
        todos.value.push ({
          id: Date.now(),
          content: newTodo.value,
          completed: false
        })
        newTodo.value = ''
      }
      function remove(item) {
        todos.value.splice(todos.value.indexOf(item), 1)
      }
      function completed(item) {
        item.completed = !item.completed
      }
      function markAll() {
        todos.value.forEach((todo) => todo.completed = true)
      }
      function removeAll() {
        todos.value.splice(0, todos.value.length);
      }

      return {
        todos,
        newTodo,
        create,
        remove,
        completed,
        markAll,
        removeAll
      }
    }
  }
</script>

<style>
*{
  margin: 0;
  padding: 0;
  font-family: 'Poppins', 'sans-serif';
}
body {
  width: 100%;
  height: 100vh;
  padding: 10px;
  background: #a9a9a9;
}
h1 {
  text-align: center;
}
.wrapper {
  background: #fff;
  max-width: 400px;
  width: 100%;
  margin: 120px auto;
  padding: 25px;
  border-radius: 5px;
  box-shadow: 0px 10px 15px rgba(0, 0, 0, 0.1);
}
input {
  width: 97%;
  margin: 20px 0;
  height: 100%;
  border-radius: 3px;
  border: 1px solid #ccc;
  font-size: 18px;
  padding: 15px 5px;
  transition: all 0.3s ease;
}
form button {
  width: 100%;
  height: 100%;
  border: none;
  color: #fff;
  margin-left: 5px;
  font-size: 21px;
  outline: none;
  background: #454548;
  cursor: pointer;
  border-radius: 3px;
  pointer-events: none;
  transition: all 0.3s ease;
}
.wrapper .todoList {
  margin-top: 20px;
  max-height: 250px;
  overflow-y: auto;
}
li {
  position: relative;
  list-style: none;
  margin-bottom: 8px;
  background: #d3d3d3;
  border-radius: 3px;
  padding: 10px 15px;
  cursor: default;
  overflow: hidden;
  word-wrap: break-word;
}
.footer {
  display: flex;
  width: 100%;
  margin-top: 20px;
  align-items: center;
  justify-content: space-between;
}
.footer button {
  padding: 6px 10px;
  border-radius: 3px;
  border: none;
  color: #fff;
  background: #295538;
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
.item {
  cursor: pointer;
}
</style>

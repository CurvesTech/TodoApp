<template>
  <div class="content-box">
    <form @submit.prevent="todoAdded">
      <input 
        type="text" 
        v-model="todo" 
        placeholder="Enter something to do..."
      >
      <button>Add</button>
    </form>
    <ul class="incomplete_list">
      <li :key="item.id" v-for="(item, index) in incompleteList">
        <input type="checkbox" v-model="item.completed">
        {{ index+1 }}. {{ item.name }}
      </li>
    </ul>
    <br>
    <h3>Completed Items</h3>
    <hr>
    <ul class="completed_list">
      <li :key="item.id" v-for="(item, index) in completedList">
       {{ index+1 }}. {{ item.name }}
      </li>
    </ul>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';

export default {
  data() {
    return {
      todo: '',
      list: []
    }
  },
  computed: {
    completedList() {
      return this.list.filter((item) => {
        return item.completed;
      })
    },
    incompleteList() {
      return this.list.filter((item) => {
        return !item.completed;
      })
    }
  },
  methods: {
    todoAdded() {
      if(this.todo.trim() !== '') {
        this.list.push({
          id: uuidv4(),
          name: this.todo,
          completed: false
        });
      }
    }
  }
}
</script>

<style scoped>
  .content-box form {
    display: flex;

  }
  .content-box > form > input {
    font-size: 24px;
    padding: 12px;
    border: 1px solid #ebebeb;
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px;
    flex: 3;
  }
  .content-box > form > input:focus {
    border: 1px solid yellow;
  }
  .content-box > form > input:active {
    border: 1px solid yellow;
  }
  .content-box > form > button {
    background: rgb(21, 21, 134);
    font-size: 24px;
    padding: 10px;
    border: none;
    color: white;
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
    flex: 1;
  }

  .content-box {
    min-height: 70vh;
    padding: 10px;
  }

  .content-box h3 {
    font-size: 22px;
  }
  .completed_list li {
    text-decoration: line-through;
    color: grey;
  }

</style>
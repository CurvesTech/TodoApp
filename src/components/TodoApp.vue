<template>
  <div class="content-box">
    <form @submit.prevent="todoAdded">
      <input 
        id="inputField"
        type="text" 
        v-model="todo" 
        placeholder="Enter something to do..."
      >
      <button>Add</button>
    </form>
    <br>
    <h3>TODO</h3>
    <hr>
    <ul class="incomplete_list">
      <template v-if="incompleteList.length > 0">
        <li :key="item.id" v-for="(item, index) in incompleteList">
          <div>
            <input @change="itemChanged" type="checkbox" v-model="item.completed">
            {{ index+1 }}. {{ item.name }}  
          </div>
          <i @click="removeItem(item.id)" class="color-red fas fa-trash-alt"></i>
        </li>
      </template>
      <template v-else>
        <div class="p-15 color-red text-center">The list is empty.</div>
      </template>
    </ul>
    <br>
    <h3>Completed Items</h3>
    <hr>
    <ul class="completed_list">
      <template v-if="completedList.length > 0">
        <li :key="item.id" v-for="(item, index) in completedList">
          <div>
            <input @change="itemChanged" type="checkbox" v-model="item.completed">
            <i>{{ index+1 }}. {{ item.name }}</i>
          </div>
          <i @click="removeItem(item.id)" class="color-red fas fa-trash-alt"></i>
        </li>
      </template>
      <template v-else>
        <div class="p-15 color-red text-center">The list is empty.</div>
      </template>

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
  watch: {
    todo(newVal) {
      localStorage.setItem('todo', newVal);
    }
  },
  mounted() {
    if(localStorage.getItem('todoList') != null) {
      this.list = JSON.parse(localStorage.getItem('todoList'));
    }
    if(localStorage.getItem('todo') != null) {
      this.todo = localStorage.getItem('todo');
    }
  },
  methods: {
    itemChanged() {
      localStorage.setItem('todoList', JSON.stringify(this.list));
    },
    removeItem(itemId) {
      this.list = this.list.filter((item) => {
        return item.id != itemId;
      });
    },
    todoAdded() {
      if(this.todo.trim() !== '') {
        this.list.push({
          id: uuidv4(),
          name: this.todo,
          completed: false
        });

        this.todo = '';

        localStorage.setItem('todoList', JSON.stringify(this.list));

        document.getElementById("inputField").focus();
      }
    }
  }
}
</script>

<style scoped>
  .p-15 {
    padding: 15px;
  }
  .color-orange {
    color: orange;
  } 
  .color-red {
    color: red;
  } 
  .text-center {
    text-align: center;
  }
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

  input[type="checkbox"] {
    margin-right: 20px;
  }

  .content-box {
    min-height: 70vh;
    padding: 20px;
  }

  .content-box h3 {
    font-size: 22px;
  }

  .incomplete_list li {
    font-size: 18px;
    font-weight: bold;
    color: rgb(17, 17, 173);
    padding: 10px;
  }
  ul li {
    display: flex;
    justify-content: space-between;
  }
  .completed_list > li > div > i {
    text-decoration: line-through;
  }

  .completed_list li {
    color: grey;
    padding: 10px;
    font-size: 18px;
  }

  ul {
    list-style-type: none;
  }

</style>
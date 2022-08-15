<template>
 <div class="todo-app">
    <ComponentHeader/>
    <component-input :list-task="listTask" :selected-task="selectedTask" @on-add-task="addTask" @on-update-task="updateTask" />
    <component-list-task :list-task="listTask" @on-edit-task="editTask" @on-delete-task="deleteTask"/>
 </div>
 <div class="text">
   <h1>First Name: {{FirstName}}</h1>
   <input v-model="FirstName" type="text">
   <button @click="changeActive()">changeActive</button>
   <button @click="changeErr()">changeErr</button>
   <div class="border" v-bind:class="objClass" ></div>
 </div>

</template>

<script>

import ComponentInput from './components/ComponentInput.vue'
import ComponentHeader from './components/ComponentHeader.vue';
import ComponentListTask from './components/ComponentListTask.vue';


export default {
  name: 'App',
  components: {
    ComponentInput,
    ComponentHeader,
    ComponentListTask
},
  data() {
     return {
      isActive: false,
      isErr: true,
       FirstName: '',
        task: '',
        selectedTask: null,
        listTask: [
        {
          id: 1,
          name: 'diy bluetooth speaker',
          status: 'todo'
        },
        {
          id: 2,
          name: 'diy handmade',
          status: 'complete'
        }
      ]
     }
},
  computed: {
    objClass() {
      return {
        active: this.isActive,
        err: this.isErr
      }
    }
  },


    methods: {

      addTask(val) {
      if(val.length == 0) return;

        this.listTask.push({
          id: this.listTask.length + 1,
          name: val,
          status: 'todo'
        })
      },

      changeActive() {
        this.isActive = !this.isActive
      },
      changeErr() {
        this.isErr = !this.isErr
      },

      editTask(id) {
        this.selectedTask = this.listTask.find(item => item.id === id);
      },

      updateTask(data) {
        if (!data || !data.id) {
          return;
        }

        this.listTask.forEach(item => {
          if (item.id === data.id) {
            item.name = data.name;
            return;
          }
        })

        this.selectedTask = null
      },

      deleteTask(id) {
        this.listTask = this.listTask.filter(item => item.id !== id)
      }
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.active {
  color: red;
}
.text {
  margin-top: 60px;
  border: 1px solid #ccc;
}
.active {
  background-color: blue;
}
.err {
  background-color: red;
}
.border {
  width: 100px;
  height: 52px;
  border: 1px solid #ccc;
}
</style>

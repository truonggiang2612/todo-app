<template>
  <div class="list-table">
    <table class="table table-bordered mt-5">

        <thead>
            <tr>
              <th scope="col">Task</th>
              <th scope="col">Status</th>
              <th scope="col" class="text-center">#</th>
              <th scope="col" class="text-center">#</th>
            </tr>
        </thead>

        <tbody v-if="listTask.length">
            <tr v-for="(task, index) in listTask" :key="index">
                <td>{{task.name}}</td>
                <td>{{task.status}}</td>
                <td>
                    <div>
                      <button @click="editTask(task.id)" class="btn-handle">EDIT</button>
                    </div>
                </td>

                <td>
                    <div>
                      <button @click="deleteTask(task.id)" class=" btn-handle">DELETE</button>
                    </div>
                </td>
            </tr>
        </tbody>

    </table>
  </div>
</template>

<script>
export default {
    name: 'ComponentListTable',
    props: {
      listTask: {
        type: Array,
        default: () => ([]),
      },
    },

    data() {
     return {
     }
    },

    methods: {
      editTask(id) {
        this.$emit('on-edit-task', id)

      },
      deleteTask(id) {
        this.$emit('on-delete-task', id)
      }
    }
}
</script>

<style>
.btn-handle {
  border: none;
  border-radius: 5px;
  transition: 0.4s;
}

.btn-handle:hover {
  background-color: #ffc107;;
}

.list-table {
  margin: auto;
  width: 80%;
}
</style>

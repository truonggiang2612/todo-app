<template>
  <div class="input-value d-flex">
    <input v-model="task"
            type="text"
            placeholder="Enter task..."
            class="form-control">

    <button v-if="!selectedTask" @click="addTask" class="btn btn-warning rounded-0">ADD</button>
    <button v-if="selectedTask" @click="updateTask" class="btn btn-warning rounded-0">UPDATE</button>
  </div>


</template>

<script>

export default {
    name: 'ComponentInput',
    props: {
      listTask: {
        type: Array,
        default: () => ([]),
      },
      selectedTask: {
        type: Object,
        default: () => ({}),
      },
    },

    data() {
     return {
        task: '',
     }
    },

    watch: {
      selectedTask: function(val) {
        this.task = val?.name || ''
      }
    },

    methods: {
      addTask() {
        this.$emit('on-add-task', this.task)
        this.task = ''
      },
      
      updateTask() {
        this.$emit('on-update-task', {
          id: this.selectedTask.id,
          name: this.task,
        })
      },

    }
}
</script>

<style scoped>
.d-flex {
  justify-content: center;
  gap: 10px;
}
.form-control {
  width: 500px;
}


</style>

<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input 
        v-model="newTask" 
        @keyup.enter="addTask()"
        class="col" 
        square 
        filled bg-color="white" 
        placeholder="Add Task" 
        dense>
        <template v-slot:append>
          <q-btn @click="addTask()" round dense flat icon="add" />
        </template>
      </q-input>
    </div>
    <q-list class="bg-white" separator bordered>
      <q-item 
        v-for="(task, index) in tasks" 
        :key="task.title" 
        @click="task.done = !task.done" 
        :class="{ 'done bg-blue-1' : task.done }"
        clickable 
        v-ripple>

        <q-item-section avatar>
          <q-checkbox v-model="task.done" class="no-pointer-events" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>

        <!-- button delete will appeared if clicked done -->
        <q-item-section
          v-if="task.done"
          side>
          <q-btn @click.stop="deleteTask(index)" flat round dense color="primary" icon="delete" />
          <!-- <q-btn label="Confirm" color="primary" @click="confirm = true" /> -->
        </q-item-section>
      </q-item>

    </q-list>

    <!-- if array empty, this will be appeared -->
    <div v-if = "!tasks.length" class="no-tasks absolute-center">
      <q-icon name="check" size="100px" color="primary" />
      <div class="text-h5 text-primary text-center">
        No tasks
      </div>
    </div>

    <!-- dialog box - triggered when click mcm modal -->
    <!-- <q-dialog v-model="confirm">
      <q-card>
        <q-card-section class="row items-center">
          <q-avatar icon="signal_wifi_off" color="primary" text-color="white" />
          <span class="q-ml-sm">You are currently not connected to any network.</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="Cancel" color="primary" v-close-popup />
          <q-btn flat label="Turn on Wifi" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog> -->
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',  
      tasks: [
        // {
        //   title: 'apple',
        //   done: false
        // },
        // {
        //   title: 'banana',
        //   done: false
        // },
        // {
        //   title: 'chocolate',
        //   done: false
        // }
      ]
    }
  },
  methods: {
    deleteTask(index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Are you sure you want to delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        // console.log('>>>> OK')
        // delete the selected index - only 1 item
        this.tasks.splice(index, 1)
        this.$q.notify('Task Deleted')
      })
    },
    addTask() {
      this.tasks.push({
        title: this.newTask,
        done: false
      })
      this.newTask = ''
    }
  }
}
</script>

<style lang="scss">
  .done {
    .q-item__label {
      text-decoration: line-through;
      color: #bbb;
    }
  }

  .no-tasks {
    opacity: 0.5;
  }
</style>

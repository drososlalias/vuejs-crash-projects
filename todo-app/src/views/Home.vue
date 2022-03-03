<template>
    <AddTask v-show="showAddTask" @add-task="addTask" />
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
</template>

<script>
import Tasks from '../components/Tasks.vue'
import AddTask from '../components/AddTask.vue'

export default {
    name:'Home',
    props: {
        showAddTask: Boolean
    },
    components:{
        Tasks,
        AddTask
    },
    data(){
        return{
            tasks: [],
        }
    },
      methods: {
    addTask(task){
      this.tasks = [...this.tasks , task]
    },
    deleteTask(id) {
      if(confirm('Are you sure?')){
        this.tasks = this.tasks.filter(task => task.id !== id);
      }
    },
    toggleReminder(id){
       this.tasks = this.tasks.map(task=> task.id === id ? {...task,reminder:!task.reminder} : task)
    }
  },
  created(){
    this.tasks = [
      {
        id:1,
        text:'Doctor Appointment',
        day: 'Monday 1st at 2:30pm',
        reminder:true
      },
      {
        id:2,
        text:'Shopping',
        day: 'Wednesday 1st at 2:30pm',
        reminder:false
      },
      {
        id:3,
        text:'Dentist',
        day: 'Monday 1st at 2:30pm',
        reminder:true
      },

    ]
  }
}

</script>
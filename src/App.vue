<template>
  <div class="container">
  <Header title="Task Tracker"/>
<!--    Set that to a methods that woukd be defined under methods at the same file-->
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
  </div>
</template>


<script>
import { Options, Vue } from 'vue-class-component';
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';

@Options({
  components: {
    Header,
    Tasks,
  },
  data() {
    return {
      tasks: []
    }
  },
 /* from each task we wanna filter, each task we want to take the id where  is not equal to the id thats passed*/
  methods: {
    deleteTask(id) {
      if(confirm("Are you sure you want to delete?")) {
    this.tasks = this.tasks.filter((task)=> task.id !== id)
      }
    },
    toggleReminder(id) {
     /* for each task (task)we do a conditional if the task.id is equal(===) to the id that's passed in*/
/*if it is (?) we want to return is an array of objects where we have the initial task {...task}properties so we can spread across the initial*/
/* and then we wanna change the reminder whatever the opposite of the current task (!task.reminder)*/
      /*else if doesn't match the id we don't want to do anything, so we return the initial task*/
      this.tasks = this.tasks.map((task)=> task.id === id ? {...task, reminder: !task.reminder}: task)
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointment',
        day: 'March 1st at 2:30pm',
        reminder: true,
      },
      {
        id: 2,
        text: 'Meeting at School',
        day: 'March 3rd at 1:30pm',
        reminder: true,
      },
      {
        id: 3,
        text: 'Food Shopping',
        day: 'March 3rd at 11:00am',
        reminder: false,
      },
    ]
  }
})
export default class App extends Vue {}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>

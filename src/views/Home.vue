<template>
    <AddTask v-if="showAddTask" @toggle-add-task="$emit('toggle-add-task')" @add-task="addTask" />

    <Tasks @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks"/>
</template>

<script>
import Tasks from '../components/Tasks';
import AddTask from '../components/AddTask'; 

export default {
    name: 'Home',
    props:{
        showAddTask: Boolean
    },
    components:{
        AddTask,
        Tasks
    },
    data(){
        return{
          tasks: []
        }
    },
    methods:{
        async deleteTask(id){
        var target = this.tasks.filter(task => task.id === id);
        if(target.length !== 0){
          var result = await fetch(`api/tasks/${id}`, {method: "DELETE"})
          result.status !== 200 ? alert('Error Deleting Task!') : console.log(`deleted ${id}`);
        }
        this.tasks = await this.fethcTasks();
      },
      async toggleReminder(id){
        var task = await this.fethcTask(id);
        var upTask = {...task, reminder: !task.reminder};
        var res = await fetch(`api/tasks/${id}`,{
          method: 'PUT',
          headers: {
            'Content-type': 'application/json'
          },
          body: JSON.stringify(upTask)
        });
        var data = await res.json();
        this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder} : task);
        console.log('toggled ', id);
      },
      async addTask(task){
        // this.tasks.push(task);
        var results = await fetch("api/tasks",{
          method: "POST",
          headers: {
            'Content-type': 'application/json'
          },
          body: JSON.stringify(task)
        });
        var data = await results.json();
        this.tasks.push(data);
      },
      async fethcTasks(){
        var result = await fetch("api/tasks");
        var data = await result.json();
        return data;
      },
      async fethcTask(id){
        var result = await fetch(`api/tasks/${id}`);
        var data = await result.json();
        return data;
      }
    },
    async created(){
    this.tasks = await this.fethcTasks();
  }
}
</script>
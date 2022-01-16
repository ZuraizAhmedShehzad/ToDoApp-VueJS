<template>
  <div class="container">
    <h2 class="text-center mt-5">My Vue Todo App</h2>
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter Task" class="form-control">
      <button @click="SubmitTask" class="btn btn-warning rounded-0">Submit</button>
    </div>

    <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task,index) in tasks" :key="index">
      <td>
        <div :class="{'finished': task.status === 'finished'}">
          {{task.name}}
        </div>
      </td>
      <td style="width:120px">
        <div @click="ChangeStatus(index)" class="pointer"
        :class="{'text-danger': task.status === 'to-do',
        'text-warning': task.status === 'in-progress',
        'text-success': task.status === 'finished'}">
          {{task.status}}
        </div>
      </td>
      <td>
        <div class="text-center" @click="EditTask(index)">
          <span class="fa fa-pen"></span>
        </div>
      </td>
      <td>
        <div class="text-center" @click="DeleteTask(index)">
          <span class="fa fa-trash"></span>
        </div>
      </td>
    </tr>
    
  </tbody>
</table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      task:'',
      editTask:null,
      availableStatuses: ['to-do','in-progress','finished'],
      tasks: [
        
      ]
    }
  },
  methods : {
    SubmitTask(){
      if(this.task.length === 0) return;
      if(this.editTask == null)
      {
        this.tasks.push({
          name:this.task,
          status:'to-do'
        })
      }
      else
      {
        this.tasks[this.editTask].name = this.task
        this.editTask = null
      }
    },
    DeleteTask(index)
    {
      this.tasks.splice(index,1)
    },
    EditTask(index)
    {
      this.task = this.tasks[index].name
      this.editTask = index
    },
    ChangeStatus(index)
    {
      let newIndex = this.availableStatuses.indexOf(this.tasks[index].status)
      if(++newIndex > 2) newIndex = 0
      this.tasks[index].status= this.availableStatuses[newIndex]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .pointer{
    cursor: pointer;
  }
  .finished{
    text-decoration: line-through;
  }
</style>

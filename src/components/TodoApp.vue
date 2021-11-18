<template>
  <div class="container">
    <h2 class="text-center mt-5"> My VueJs TodoApp !!! </h2>

    <!-- inpputs -->
    <div class="d-flex mt-5">
      <input type="text" name="" v-model="task" class="form-control" placeholder="Enter text" id="">
      <button class="btn btn-warning rounded-0" @click="createNew"> Submit </button>
    </div>
  
  <!-- Tasks Table -->
  <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col"> Task </th>
      <th scope="col"> Status </th>
      <th scope="col" class="text-center"> # </th>
      <th scope="col" class="text-center"> # </th>
    </tr>
  </thead>
  <tbody>
    <tr class="p-3" v-for=" task,index in tasks" :key="index">
      <th> {{task.name}} </th>
      <td class="" style="font-weight:bolder;"> <span @click="changeStatus(index)" class="pointer"> {{task.status}}</span> </td>
      <td class="p-3">
        <div class="text-center" @click="editTask(index)">
          <i class="fas fa-edit"></i>
        </div>
      </td>
      <td class="p-3">
        <div class="text-center" @click="deleteTask(index)">
          <i class="fas fa-trash"></i>
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
    return{
      editedtask:null,
      task: '',
      availablestatuses:['To-do', 'In-progress','Finished'],
      tasks:[
        {name:'Steal bananas from the store.', status:'to-do'},
        {name:' Eat 1KG chocolate within one hour. ', status:' In-progress'},
      ]
    }
  },
  methods:{
    createNew(){
      if(this.task.length !== 0){
        if(this.editedtask === null){
          this.tasks.push({name:this.task, status:'To-do'})  
          this.task = ''
          return true
        }else{
          this.tasks[this.editedtask].name = this.task
        }
      }
    },
    deleteTask(index){
      this.tasks.splice(index, 1)
    },
    editTask(index){
      this.task = this.tasks[index].name
      this.editedtask = index
    },
    changeStatus(index){
      let newIndex = this.availablestatuses.indexOf(this.tasks[index].status)
      if(++newIndex > 2) newIndex = 0
      this.tasks[index].status = this.availablestatuses[newIndex]
    }
  }
};
</script>

<style scoped>
.pointer{
  cursor: pointer;
}
</style>

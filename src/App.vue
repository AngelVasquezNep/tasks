<template>
  <div id="app">
    <!-- <p>Soy: {{name}}</p> -->
      <div id="banner" >
        <img src="dist/background.jpg" alt="image background">
        <label class="banner" for="tasktitle">Add your task</label>
      </div>

      <h1>Notes by {{name}}</h1><span class="change" @click="changeUser">↺</span>

      <div class="" v-show="!saved">
        <input type="text" v-model="name" name="" value="" ><button type="button" name="button" @click="saveUser">Save</button>
      </div>

      <form id="formu"  @submit.prevent="addTask" action="index.html" method="post">
        <div class="">
          <label for="tasktitle">New Task: </label>
          <input type="text" id="tasktitle" v-model="newTask.title"required name="" value="" placeholder="Enter your task"size="27">
        </div>
        <div class="">
          <label for="tasktime">Time: </label>
          <input type="number" min="1" id="tasktime" v-model="newTask.time" required name="" value="0" class="rangeTime">
        </div>
          <!-- <br> -->
        <div class="">
          <input type="submit" name="" class="addTask" value="AddTask">
          <input type="button" name="" @click="cancel" value="Cancel">
        </div>

      </form>

      <p>Tasks: {{totalTask}} | Total time: {{totalTime}} hour<span v-show="totalTask>1">s</span> </p>

      <div class="contentTask">
        <h2 v-show="totalTask<1">Everything OK</h2>
        <div v-for="(t,index) in tasks">
          <div class="tasks":key="t.index">

            <input type="button" class="delete" @click="removeTask(index)" name="" value="Delete Task">
            <span id="titulos">
              <p>Title: {{t.title}}</p>
            </span>
            <span>
              <p>Time: {{t.time}} hour<span v-show="t.time>1">s</span></p>
            </span>

          </div>
        </div>
      </div>

      <footer>
        <p>Thank you for visiting us.</p>
        <p>By Angel Vasquez</p>
        <a href="https://github.com/AngelVasquezNep" target="_blank">GitHub</a>
        <a href="https://twitter.com/angelvasqueznep" target="_blank">Twitter</a>
      </footer>

</div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      name: '',
      newTask:{title:"", time:0},
      tasks:[],
      saved: true
    }
  },
  methods:{
    addTask(){
      this.tasks.push(this.newTask)
      this.newTask={title:"", time:0}
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
    },
    cancel(){
      this.newTask={title:"", time:0}
    },
    removeTask(index){
      console.log(index)
      this.tasks.splice(index,1)
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
    },
    saveUser(){
      this.saved=true
      localStorage.setItem('name', JSON.stringify(this.name))
    },
    changeUser(){
      this.saved=false
      localStorage.setItem('name', JSON.stringify(this.name))
    }

  },
  computed:{
    totalTime(){
      return this.tasks.reduce((resultado, task)=>{
        resultado += parseInt(task.time)
        return resultado
      }, 0)
    },
    totalTask(){

      return this.tasks.length
    }
  },
  created: function(){
    this.tasks = JSON.parse(localStorage.getItem('tasks')) || []
    this.name = JSON.parse(localStorage.getItem('name')) || 'YOUR NAME'
  },
  watch:{

  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    align-items: center;
    justify-content: center;
    background: rgb(222, 224, 193);
  }
  .banner{
    position: absolute;
    top: 0;
    left: 0;
    background: rgba(1, 210, 160, .7);
    padding: 10px;
    margin: 10%;
    font-size: 3.5rem;
    color:white;
    border-radius: 1rem;
    cursor: pointer;
  }
  .contentTask{
    border-top: solid grey;
    border-bottom: solid grey;
    padding: 10px;
    background: rgb(247, 246, 241);
  }
  .tasks{
    display: flex;
    justify-content: space-around;
    align-items: center;
    margin: 10px;
    background: rgb(32, 190, 128);
    text-align: center;
    border-radius: 1rem;
  }
  .tasks span{
    border-radius: 1rem;
    margin: 3px 0;
    align-items: center;
    background: white;
    min-height: 50px;
    text-align: center;
    width: 15%;
  }
  .tasks #titulos{
    width: 60%;
  }

  .delete{
    height: 50px;
    border-radius: 1rem;
    border-style: none;
    margin: 1rem 0;
    width: 20%;
    color: white;
    background-color: rgb(39, 131, 101);
    cursor:pointer;
  }
  .change{
    background: rgb(72, 201, 151);
    font-size: 1.2rem;
    margin: 3px;
    padding: 3px;
    border-radius: 20%;
    cursor: pointer;
  }

  .addTask{
    background: rgb(44, 172, 118);
    border-style: none;
    padding: 5px;
    border-radius: 1rem;
    cursor: pointer;
  }
  .rangeTime:out-of-range{
    background-color: rgba(255, 0, 0, 0.42);
    border-style: none;
    color:rgb(255, 255, 255);
  }


  footer{
    background: rgb(32, 190, 128);
    margin: 0;
    width: 100%;
    display: flex;
    padding: 1.5rem 0;
    flex-direction: column;
    align-items: center;
    justify-content:center;
    min-height: 120px;
    color: rgb(255, 255, 255);
    margin-top: 3rem;
  }
  h1{
    display: inline-block;
  }
  img{
    width: 100%;
    position: relative;
  }
  li{
    list-style: none;
  }
  a{
    text-decoration: none;
    margin: 5px 0;
  }
  form{
    align-items: center;
    justify-content: center;
    margin: 3rem 0;
    display: flex;
    flex-wrap: wrap;
  }
  form>*{
    margin: 10px 0;
  }
  input{
    margin: 5px;
    transition: .2s;
  }

  input[type="button"], input[type="submit"], input[type="text"], input[type="number"]{
    font-size: 1em;
  }

  @media screen and (max-width: 900px){
    .banner{
      display: none;
    }
  }



</style>

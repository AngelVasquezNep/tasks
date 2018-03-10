<template>
  <div id="app">
    <!-- <p>Soy: {{name}}</p> -->
      <div id="banner" >
        <img src="dist/background.jpg" alt="image background">
        <div class="banner" @click="bajar">
          Add your task
        </div>
      </div>

      <h1 id="tasks">Notes by {{name}}</h1>
      <span class="change" @click="changeUser">↺</span>

      <div class="" v-show="!saved">
        <input type="text" v-model="name" name="" value="" >
        <button name="button" @click="saveUser" class="save">Save</button>
      </div>

      <form id="formu"  @submit.prevent="addTask" action="index.html" method="post">
        <div class="">
          <label for="tasktitle">New Task: </label>
          <input type="text" id="tasktitle" v-model="newTask.title" required name="" value="" placeholder="Enter your task" size="27">
        </div>
        <div class="">
          <label for="tasktime">Time: </label>
          <input type="number" min="1" id="tasktime" v-model="newTask.time" required name="" value="1" class="rangeTime">
        </div>
          <!-- <br> -->
        <div class="botones">
          <input type="submit" name="" class="addTask" value="AddTask">
          <input type="button" name="" @click="cancel" value="Cancel">
        </div>

      </form>

      <p>Tasks: {{totalTask}} | Total time: {{totalTime}} hour<span v-show="totalTask>1">s</span> </p>

      <div class="contentTask">
        <h2 v-show="totalTask<1">Everything OK</h2>
        <div v-for="(t,index) in tasks" :key="t.index">
          <div class="tasks" >

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
        <a href="https://github.com/AngelVasquezNep" target="_blank">
        <span><img src="./assets/github.png" alt="github"></span>GitHub
        </a>
        <a href="https://twitter.com/angelvasqueznep" target="_blank">
        <span><img src="./assets/twitter.png" alt="github"></span>Twitter
        </a>
      </footer>

</div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      name: '',
      newTask:{title:"", time:''},
      tasks:[],
      saved: true
    }
  },
  methods:{
    addTask(){
      this.tasks.push(this.newTask)
      this.newTask={title:"", time:''}
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
    },
    cancel(){
      this.newTask={title:"", time:''}
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
    },
    bajar(){
      const $objetivo = document.getElementById("tasks")
      $objetivo.scrollIntoView({
          behavior: "smooth",
          block: "start"
      })
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
    font-family: 'Lato', sans-serif;
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
    border-radius: 1rem;
    cursor: pointer;
    color:white;
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
    font-size: 1.4rem;
    margin: 10px;
    padding: 6px;
    border-radius: 20%;
    cursor: pointer;
    transition: all .3s;
  }

  .change:hover{
    background-color: rgb(31, 135, 95) ;
    color: #fff;
  }

  .change:active{
    font-size: .95rem;
  }

  .addTask, .save{
    background: rgb(44, 172, 118);
  }
  .rangeTime:out-of-range{
    background-color: rgba(202, 9, 9, 0.192);
    border-style: none;
    color:rgb(255, 255, 255);
  }


  footer{
    background: rgb(32, 190, 128);
    margin: 0;
    width: 100%;
    display: flex;
    padding: 1rem 0;
    /* flex-direction: column; */
    align-items: center;
    justify-content:center;
    min-height: 20px;
    color: rgb(255, 255, 255);
    margin-top: 3rem;
  }
  footer p, footer a, footer span {
    padding: 10px 20px
  }

  footer span img {
    width: 16px;
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
    margin: 10px 0;
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
    outline: none;
  }
  input[type="text"], input[type="number"]{
    border-radius: .5rem;
    padding: 5px;
    border: 0;
  }

  input[type="button"], input[type="submit"], input[type="text"], input[type="number"]{
    font-size: 1em;
  }

  button, input[type="button"], input[type="submit"]{
    font-size: 1em;
    padding: 7px;
    color: #fff;
    border: 0;
    outline: none;
    cursor: pointer;    
    border-radius: 10px;
    transition: all .2s;
    border-bottom: 3px solid #808080;
  }

  input[type="button"]{
    background-color: rgb(189, 35, 61);
    border-bottom: 3px solid rgb(192, 33, 81);
  }  

  input[type="button"]:hover{
    background-color: rgb(145, 20, 41);
  }

  button:hover, 
  input[type="button"]:hover, 
  input[type="submit"]:hover{
    box-shadow: 0 2px 2px 1px #2c3e50;
    border-bottom: 3px solid #2c3e50;
  }

  button:active, 
  input[type="button"]:active, 
  input[type="submit"]:active{
    transform: scale(.95);
  }

  input:focus {
    box-shadow: 0 0 0 2px  aqua;
  }

  @media screen and (max-width: 900px){
    .banner{
      display: none;
    }
  }



</style>

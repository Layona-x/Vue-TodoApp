<script>
  const date = new Date();
  const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
  
 export default {
   data(){
    return {
      todos:[],
      newTodoTitle:"",
      newTodoDescription:""
     }
   },
   methods:{
   addTodo(){
     console.log(this.todos)
    this.todos.push({
     title:this.newTodoTitle,
     description:this.newTodoDescription,
     done:false,
     date:date.toLocaleDateString('tr-TR', options)
   })
     this.newTodoTitle = ""
     this.newTodoDescription = ""
   },
  deleteTodo(index){
     this.todos.splice(index,1)
  },
  doneTodo(index){
     const todo = this.todos[index]
     todo.done = !todo.done
   }
  },
   mounted(){

  const todoStorage = localStorage.getItem("Todo")
  const todoy =  JSON.parse(todoStorage ? todoStorage : [])
  this.todos = todoy
   },
   watch:{    
    todos:{
      deep:true,
      handler(){
     const todos = this.todos
        localStorage.setItem("Todo",JSON.stringify(todos))
      }
    }
  }
 }
</script>

<template>
  <head>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.2.0/css/all.min.css" integrity="sha512-xh6O/CkQoPOWDdYTDqeRdPCVd1SpvCA9XXcUnZS2FmJNp1coAFzvtCN9BmamE+4aHK8yyUHUSCcJHgXloTyT2A==" crossorigin="anonymous" referrerpolicy="no-referrer" />
  </head>
  <body>
<form @submit.prevent="addTodo" class="todo">
 <input v-model="newTodoTitle" type="text" class="todo-input" placeholder="Görevinizin Başlığını Giriniz">
 <input v-model="newTodoDescription" type="text" class="todo-input" placeholder="Görevinizin Açıklamasını Giriniz">
<button type="submit" class="todo-button">Ekle</button>
</form>
   <div v-for="(todo,index) in todos" :key="index" class="card-1 card">
        <div class="col card__icon">
        <p class="col card__exit"><i @click="deleteTodo(index)" class="fas fa-times"></i><br><i style="margin-top:100px;margin-right:90px" class="fa-solid fa-circle-check" @click="doneTodo(index)"></i>
        </p>
        </div>
      <div :class="{'done': todo.done}"><h2 style="color:white" :class="card__title"><b>{{ todo.title }}</b></h2></div>
        <div class="card__link">{{ todo.description}}</div>
        <p class="card__apply">
          {{todo.date}}</p>
      </div>
  </body>
</template>

<style>
  .col{
    color:white;
    margin-left:90%;
    position:absolute;
    margin-right:20px
  }
  .done{
   text-decoration:line-through
  }
  .todo{
   display:block;
  }
  .todo-input{
  margin-right:2.5%;
  width:95%;
  border:2px black solid;
  height:30px;
  margin-top:10px;
  border-radius:10px;
  }
 .todo .todo-input::placeholder{
  font-weight:50;
  color:black;
  margin-right:20px
 }
 .todo-button{
  height:35px;
  width:120px;
  margin-right:20px;
  margin-top:10px;
  align-items:center;
  color:white;
  background:#3498db;
  border:none;
  border-radius:10px;
  display:block;
 }
 .card{
   height:200px;
   margin-top:20px;
   border-radius:30px;
   background:#34495e;
   display:flex;
   justify-content:space-between;
 }
 .todo-data h1{
   margin-left:50%;
   color:white;
   margin-top:3px;
  }
  .todo-status{
  position:absolute;
  right:0;
  display:block;
  margin-top:50px;
  }
  *{
   margin:0;
   padding:0;
   box-sizing:border-box
  }
  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica,
      Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
      background-color: #7f8c8d
  }
  
  .main-container {
    padding: 30px;
  }
  
  /* HEADING */
  
  .heading {
    text-align: center;
  }
  
  .heading__title {
    font-weight: 600;
  }
  
  .heading__credits {
    margin: 10px 0px;
    color: #888888;
    font-size: 25px;
    transition: all 0.5s;
  }
  
  .heading__link {
    text-decoration: none;
  }
  
  .heading__credits .heading__link {
    color: inherit;
  }
  
  /* CARDS */
  
  .cards {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  
  .card {
    padding:20px;
    width: 500px;
    min-height: 200px;
    display: grid;
    grid-template-rows: 20px 50px 1fr 50px;
    border-radius: 10px;
    box-shadow: 0px 6px 10px rgba(0, 0, 0, 0.25);
    transition: all 0.2s;
  }
.card:hover {
    box-shadow: 0px 6px 10px rgba(0, 0, 0, 0.4);
  }
  .card-exit .fa-times{
   position: absolute;
   right: 0px;
    text-decoration: none;
    color: rgba(255, 255, 255, 0.9);
  }
  .card__link
  {
    margin-top:40px;
    position: relative;
    text-decoration: none;
    color: rgba(255, 255, 255, 0.9);
  }
  
  .card__link::after {
    position: absolute;
    top: 25px;
    left: 0;
    content: "";
    width: 0%;
    height: 3px;
    background-color: rgba(255, 255, 255, 0.6);
    transition: all 0.5s;
  }
  
  .card__link:hover::after {
    width: 100%;
  }
  .card__substext{
    color: rgba(255, 255, 255, 0.9);

  }
  .card__exit {
    grid-row: 1/2;
    justify-self: end;
  }
  
  .card__icon {
    display:block;
    position:absolute;
    grid-row: 2/3;
    font-size: 30px;
  }
  
  .card__title {
    grid-row: 3/4;
    font-weight: 400;
    color: #ffffff;
  }
  
  .card__apply {
    grid-row: 4/5;
    align-self: center;
    color: floralwhite;
  }
  
  /* CARD BACKGROUNDS */
  
  .card-1 {
    background: radial-gradient(#2c3e50, #2c3e50);
  }
  
  .card-2 {
    background: radial-gradient(#fbc1cc, #fa99b2);
  }
  
  .card-3 {
    background: radial-gradient(#76b2fe, #b69efe);
  }
  
  .card-4 {
    background: radial-gradient(#60efbc, #58d5c9);
  }
  
  .card-5 {
    background: radial-gradient(#f588d8, #c0a3e5);
  }
  
  /* RESPONSIVE */
  
  @media (max-width: 1600px) {
    .cards {
      justify-content: center;
    }
    .col {
      margin-right:10%
    }
  }

</style>
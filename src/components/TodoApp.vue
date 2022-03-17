<template>
 <div class="todo-app">
     <h1>TODO APPLICATION</h1>
   <form @submit.prevent="AddTodo">
   
<input type="text" v-model="TempTodo">



<button @click="AddTodo" type="button" class="btn btn-primary add">Add Todos</button>

 </form >
 

 <div class="output">
   <ul>
     <li v-for="(todo, n) in Todos" :key="todo.index">
       <input type="checkbox" name="" id="" v-model="todo.collected" @change="SaveTodo"> <!--Update the Value of collected with V-model-->
       <span v-bind:class="{collected:todo.collected}">{{todo.name}}</span>
       <button @click="DeleteTodo(n)" type="button" class="btn btn-danger delete">Delete</button>
     </li>
   </ul>
   
   <button id="center" @click="ClearAll" type="button" class="btn btn-success clear">Clear All</button>
 </div>

 </div>
</template>

<script>
export default {
  
  data(){
    return{
      TempTodo:"",
      Todos:[
        {name:"Learn Html", collected:false},
        {name:"Learn Css", collected:false}
      ],
    }
  },
  methods:{
ClearAll(){
  this.Todos=[]
  this.SaveTodo()},
DeleteTodo(n){
  this.Todos.splice(n,1)
  this.SaveTodo()
},
AddTodo(){
  if (this.TempTodo !== ""){
 this.Todos.push({
   name:this.TempTodo,
   collected:false
 })
  this.TempTodo=""
  this.SaveTodo()
  }
 
},
SaveTodo(){
    localStorage.Todos=JSON.stringify(this.Todos)
},

  },
  mounted(){
if(localStorage.Todos){
    this.Todos = JSON.parse(localStorage.Todos)
}
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  margin: 10px;
  padding: 1.4rem;
  font-size: 1.8em;
  
  
}

a {
  color: #42b983;
}
.todo-app{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    border: 5px solid black;
    max-width: 65ch;
    height: 75vh;
    margin: 0 auto;
    justify-content: start;
    align-items: flex-start;
    align-content: flex-start;
     border-radius: 10px;
}
span.collected{
    text-decoration: line-through;
   
}

h1{
    grid-column: 1/5;
    text-shadow: 2px 2px 2px #CE5937;
    color: lawngreen;

text-shadow: 0 -1px 4px #FFF, 0 -2px 10px #ff0, 0 -10px 20px #ff8000, 0 -18px 40px #F00;
}

form{
     grid-column: 1/5;
    
}
.output{
 grid-column: 1/5;
 display: grid;
 grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
 grid-template-rows: minmax(10px, 6);
}
ul{
     grid-column: 1/6;
    grid-row: 4/4;
    display: grid;
    flex-direction: column;
}
li{
    grid-column: 1/6;
}

ul input{
    float: left;
     margin: 18px;
  padding: 1.9rem;
  font-size: 1.8em;
 
  
    }

    ul button{
        float: right;
    }
    

.clear{
    grid-column: 3/5;
    grid-row: 5/5;
}
.add{
    margin-left: 60px;
}
form input{
    
    border-radius: 10px;
}


</style>

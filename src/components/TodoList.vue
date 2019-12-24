<template>
    <div id="main">
        <header>
            <h1>Todo List</h1>
        </header>
        
        
        <div>
             
            <label><input type= "checkbox"  v-model="showComplete"/><strong>Show Completed </strong></label>
        </div>
        <div>
            <ul>
                <li class="list" v-for="todo in filteredList" v-bind:Key="todo.text">
                    <label>
                        <input type="checkbox" v-model="todo.isComplete"/>
                        <span v-bind:class="{completed:todo.isComplete}">{{todo.text}}</span>
                    </label>
                </li>
              
            </ul>
        </div>
        <br>
        <div>
            <form v-on:submit.prevent="addTodo">
                <input type="text" v-model="taskName" class="inputBox" placeholder="Add new item">
                <br>
                <button >Add Todo</button>
            </form>
        </div>
        
    </div>
</template>

<script>

let todos = [
    {
        text: 'making tea',
        isComplete: false
    },
    {
        text: 'making breakfast',
        isComplete: true
    }
];

export default {
    name: 'TodoList',
    data(){
        return{
            taskName: '',
            todos,
            showComplete: true
        }
    },
    computed:{
        filteredList(){
            return this.todos.filter(todo => this.showComplete ? true : !todo.isComplete);
        }

    },
    methods:{
        addTodo(){
           todos.push({
               text: this.taskName,
               isComplete: false
           })
          
          this.taskName = '';
        }
    }
}
</script>

<style scoped>
#main{
    width: 500px;
    margin: auto;
    font-family:Georgia, 'Times New Roman', Times, serif;
}

header{
    background-color: chartreuse;
    text-align: center;
}

ul{ 
    padding: 0;
    cursor: pointer;
}

.list{
    width: 95%;
    border: 1px solid gray;   
    list-style: none;
    text-align: left;
    float: left;
    padding: 10px;
    border-radius: 5px;
}
.inputBox{
    width: 95%;
    padding: 10px;
    margin-top: 20px;
    margin-bottom: 5px;
    border: 1px solid gray;
    border-radius: 5px;
}

button{
    background-color: darkcyan;
    padding: 10px;
    border: 1px solid black;   
    border-radius: 5px;
    
}

.completed{
    font-style: italic;
    text-decoration: line-through;
    color: gray;
}

</style>
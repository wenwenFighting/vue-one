<template>
  <div id="hello">
    <header>{{msg}}</header>
    <input type="text" class="fm_new" placeholder="添加一个任务..." v-model="newTodo" @keyup.enter="addTodo">

    <section class="ctrl" v-show="todos.length">
        <span class="tip">1项剩余</span>
        <span class="type">全部</span>
        <span class="type">未完成</span>
        <span class="type">已完成</span>
        <span class="clear_all">清除已完成</span>
    </section>
    <section class="main">
        <div class="item" v-for="(todo,index) in todos" :class="{finish:todo.completed,editing:edited == todo}">
            <span @click="finishTodo(todo)"></span>
            <p @dblclick="changeTodo(todo)">
                {{todo.title}}
            </p>
            <input type="text" class="edit" v-model="todo.title">
            <em @click="removeTodo(index)"></em>
        </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to my Vue.js App',
      newTodo:'',
      todos:[],
      edited:null
    }
  },
  methods: {
    addTodo() {
      if(this.newTodo && this.newTodo.trim()){
        this.todos.push({title:this.newTodo,completed:false});
        this.newTodo = '';
      }else{
        return;
      }
    },
    removeTodo(index) {
      this.todos.splice(index,1);
    },
    finishTodo(todo) {
      todo.completed = !todo.completed;
    },
    changeTodo(todo) {
      this.beforeEditCache = todo;
      this.edited = todo;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*{
    margin: 0;
    padding: 0;
}
body{
    background: #eee;
    color: #666;
    -webkit-font-smoothing: antialiased;
}
header{
    font-size: 40px;
    color: rgba(175, 47, 47, 0.15);
    text-align: center;
    margin-top: -100px;
}
input{
    display: block;
    outline: none;
    border: none;
    color: #666;
}
.fm_new{
    width: 500px;
    height: 40px;
    padding: 0 10px;
    background: #fff;
    border-radius: 3px;
    box-shadow: 0 1px 1px rgba(0,0,0,.1);
    margin: 20px auto 0;
    font-size: 18px;
}

.main{
    width: 500px;
    background: #fff;
    box-shadow: 0 1px 1px rgba(0,0,0,.1);
    border-radius: 3px;
    padding: 0 10px;
    margin: 20px auto 0;
}
.item{
    height: 50px;
    line-height: 50px;
    position: relative;
    border-bottom: 1px solid #f2f2f2;
}
.item:last-child{
    border-bottom: none;
}
.item:after{
    content: '';
    display: block;
    clear: both;
}
.item span{
    display: block;
    width: 20px;
    height: 20px;
    border: 1px solid #dce0e3;
    background-color: #fff;
    border-radius: 100%;
    margin-right: 5px;
    position: relative;
    top: 13px;
    float: left;
}
.item.finish span:after{
    content: '';
    width: 16px;
    height: 16px;
    position: absolute;
    top: 2px;
    left: 2px;
    background-color: #0099e5;
    border-radius: 100%;
}
.item p{
    height: 25px;
    float: left;
    margin-left: 10px;
}
.item.finish p{
    text-decoration: line-through;
    color: #ddd;
}
.item p i{
    font-size: 12px;
    font-style: normal;
    color: #999;
    position: relative;
    top: -2px;
}
.item em{
    width: 30px;
    height: 30px;
    float: right;
    cursor: pointer;
    display: none;
    position: relative;
    top: 10px;
}
.item:hover em{
    display: block;
}
.item em:before,.item em:after{
    content: '';
    display: block;
    width: 25px;
    height: 1px;
    background: #cc9a9a;
    position: relative;
    top: 13px;
}
.item em:before{
    transform: rotate(45deg);
}
.item em:after{
    transform: rotate(-45deg);
}
.ctrl{
    width: 500px;
    text-align: center;
    margin: 20px auto 0;
    font-size: 14px;
}
.ctrl .tip{
    float: left;
}
.ctrl .type{
    display: inline-block;
    cursor: pointer;
    margin: 0 4px;
}
.ctrl .type.on{
    color: #0099e5;
}
.ctrl .clear_all{
    float: right;
    cursor: pointer;
}
.edit{
  display:none;
}
.editing .edit{
  display: block;
  width: 506px;
  padding: 15px 16px;
  margin: 0px 0 0 20px;
  position: absolute;
  font-size: 16px;
}
</style>

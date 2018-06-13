<template>
  <div class="mainApp">
    <div is="addTodo" @add="add"></div>
    <div is="viewStateController" @click.native="changeViewState" :view_state="viewState"></div>
    <ul class="todoList">
      <li is="listItem" v-for="(task,index) in todoList" :task="task" :index="index" :view_state="viewState"
          @change_task_state="changeTaskState" @del_task="delTask"></li>
    </ul>
  </div>
</template>

<script>
  import addTodo from "./addTodo/addTodo.vue"
  import viewStateController from "./viewState.vue"
  import listItem from "./todoList/item.vue"

  export default {
      data(){
          return {
                  willAddTask:{
                      title:"",
                      state:"unfinished",
                      content:"",
                      ifShowDetail:false,
                  },
                  todoList:[
                     /* {
                          title:"单机版的tudoList",
                          content:"+++",
                          state:"unfinished",
                      },
                      {
                          title:"tudoList",
                          content:"+++",
                          state:"finished",
                      },*/
                  ],
                  viewState:"all"
          }
      },
      methods:{
          add:function(task){
              this.todoList.unshift(task)
          },

          changeTaskState(i){
              let task = this.todoList[i];
              if(task.state === "unfinished"){
                  /*要直接修改todoList，而不是修改某个元素的某个属性，不然不会触发UI层的变化*/
                  let new_task = this.todoList.splice(i,1)[0]
                  new_task.state = "finished"
                  this.todoList.splice(i,0,new_task)

              }else if (task.state === "finished"){
                  let new_task = this.todoList.splice(i,1)[0]
                  new_task.state = "unfinished"
                  this.todoList.splice(i,0,new_task)

              }else {
                  console.log("未经过流程",this.todoList[i])
              }
          },
          delTask(i){
              this.todoList.splice(i,1)
          },

          changeViewState(e){
              this.viewState = e.target.innerText
          },
      },
      components:{
          addTodo:addTodo,
          viewStateController,
          listItem
      },
      created(){
          if(localStorage.$__todoList == undefined){
              this.todoList = []
          }else {
              this.todoList = JSON.parse(localStorage.$__todoList)
          }
      },
      updated(){
          localStorage.$__todoList = JSON.stringify(this.todoList)
      }
  }
</script>

<!--css 模块化。。。-->
<style scoped lang="less">
  @app_width:620px;
  @app-margin-top:20px;
  .mainApp{
      padding: 10px;
      width:@app_width;
      height: 1500px;
      margin: @app-margin-top auto 0px;
  }
</style>

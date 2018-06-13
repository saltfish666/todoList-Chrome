<template >
    <li  v-if=" view_state == 'all'  || task.state == view_state" class="list-item">
        <div class="titleArea">
            <span :class="{del:(task.state=='finished')}">{{task.title}}</span>
            <button  class="detail" @click="showDetail()">{{ifShowDetail ? "隐藏详情":"显示详情"}}</button>
            <button  class="complete"@click="changeTaskState(index)">{{(task.state == "unfinished")?"完成任务":"取消完成"}}</button>
            <button  class="delete" @click="delTask(index)">删除任务</button>
        </div>
        <div v-text="task.content"  v-show="ifShowDetail" :class="{del:(task.state=='finished')}"></div>
    </li>
</template>

<script>
    export default {
        props:["task","index","view_state"],
        data:function(){
            return {
                ifShowDetail:false
            }
        },
        methods:{
            changeTaskState(index){
                this.$emit("change_task_state",index)
            },
            delTask(index){
                this.$emit("del_task",index)
            },
            showDetail(){
                this.ifShowDetail = !this.ifShowDetail
            }
        }
    }
  /*  let listItem = {
        props:["task","index","view_state"],
        data:function(){
            return {
                ifShowDetail:false
            }
        },
        template:"#listItem",
        methods:{
            changeTaskState(index){
                this.$emit("change_task_state",index)
            },
            delTask(index){
                this.$emit("del_task",index)
            },
            showDetail(){
                this.ifShowDetail = !this.ifShowDetail
            }
        }
    };
    Vue.component("listItem",listItem)*/
</script>

<style scoped="" lang="less">
    .list-item {
        list-style: none;
        margin: 20px 0px;

        .titleArea {
            display: flex;
            height: 30px;
            align-items: center;

            span {
                margin: 0px;
                width: 400px;
                font-weight: 900
            }

            @button-width: 70px;
            .detail {
                background-color: olivedrab;
                color: white;
                height: 25px;
                width: @button-width;
                margin-right: 10px;
                border-radius: 8px;
            }
            .complete {
                background-color: green;
                color: white;
                height: 25px;
                width: @button-width;
                margin-right: 10px;
                border-radius: 8px;
            }
            .delete {
                background-color: #f46258;
                color: white;
                height: 25px;
                width: @button-width;
                padding-right: 10px;
                border-radius: 8px;
            }

        }
    }

    .del{
        text-decoration:line-through;
        color:#cce6ff
    }

</style>

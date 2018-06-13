<template >
    <div class="addTask">
        <input type="text" v-model="title" placeholder="事务标题">
        <textarea v-model="content" placeholder="事务内容"></textarea>
        <button @click="add">添    加    事    务</button>
    </div>
</template>
<script>
    export default {
        data:function(){
            return {
                title:"",
                content:"",
                state:"unfinished",
            }
        },
        methods:{
            add(){
                if(!this.title){
                    return
                }
                let task={
                    title:this.title,
                    content:this.content,
                    state:this.state,
                }
                this.$emit("add",task)
                this.title = ""
                this.content = ""
            }
        }
    }
/*    Vue.component("addTodo",{
        template:"#addTodo",
        data:function(){
            return {
                title:"",
                content:"",
                state:"unfinished",
            }
        },
        methods:{
            add(){
                if(!this.title){
                    return
                }
                let task={
                    title:this.title,
                    content:this.content,
                    state:this.state,
                }
                this.$emit("add",task)
                this.title = ""
                this.content = ""
            }
        }
    })*/
</script>
<style scoped="" lang="less">
    .addTask{
        @input-height:32px;
        @input-width:99%;       //不然边界会溢出？
        @input-fontSize:18px;
        input{
            display: block;
            height: @input-height;
            width: @input-width;
            font-size: @input-fontSize;
        }
        @textarea-height:130px;
        @textarea-fontSize:15px;
        textarea{
            display: block;
            height: @textarea-height;
            width: @input-width;
            font-size: @textarea-fontSize;
            margin:10px 0px;
        }
        @button-height:30px;
        @button-fontSize:15px;
        button{
            width:100%;
            height: @button-height;
            font-size: @button-fontSize;
            background-color: #586df4;
            color: white;
            margin: 10px 0px;
            border-radius: 10px;
        }
    }
</style>

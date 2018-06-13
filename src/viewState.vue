<template id="viewStateController">
    <div class="state">
        <span :class="{active:(view_state=='all')}">all</span>
        <span :class="{active:(view_state=='finished')}">finished</span>
        <span :class="{active:(view_state=='unfinished')}">unfinished</span>
    </div>
</template>
<script>
    export default {
        props:["view_state"],
    }
</script>
<style scoped="" lang="less">
    .active{
        color: white;
        background-color: green;
        border-radius: 4px;
    }

    .state {
        display: flex;
        align-items: center;
        padding: 0px 20px;
        margin-top: 10px;
        margin-bottom: 20px;
        span {
            padding: 4px 80px;
            font-size: 15px;
            border-radius: 20px;
        }
    }
</style>

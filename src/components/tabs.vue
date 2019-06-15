<template>
    <ul id="tabs">
        <li 
            v-for="(tab,index) of tabItems"
            :key="index"
            @click="switchTab($event,tab,index)"
            :class="index === currActive?'active':''"
        >{{tab}}</li>
    </ul>
</template>

<script>
export default {
    data(){
        return {
            tabItems:['all','active','completed'],
            currActive:0
        }
    },
    methods:{
        switchTab(event,tab,index){
            this.currActive = index;
            this.$emit('switchTab',tab)
        }
    }
}
</script>

<style lang="scss" scoped>
    #tabs{
        li{
            border-radius:5px;
            float: left;
            text-align: center;
            margin-right: 10px;
            padding:0 10px;
            border: 1px solid rgba(231, 109, 93 ,0);
            cursor: pointer;
        }
        .active{
            border: 1px solid rgba(231, 109, 93 , 1)
        }
    }
</style>




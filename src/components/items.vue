<template>
    <ul class="items">
        <li 
            v-for="(item,index) of itemData"
            :key="index"
        >
            <img 
                class="item-icon" :src="getPath(item.state)" 
                @click="$emit('changState',[item.id
                    ,item.state === 'active'?'completed':'active'])"
            />
            <span>{{item.content}}</span>
            <img 
                class="item-remove" 
                src="../assets/images/closer.svg"
                @click="$emit('remove',index)"
            >
        </li>
    </ul>
</template>

<script>
export default {
    props:{
        itemData:{
            type:Array,
            required:true
        }
    },
    data(){
        return{
            
        }
    },
    methods:{
        getPath(state){
            let path = '';
            if(state === 'active'){
                path = require('../assets/images/round.svg')
            }else{
                path = require('../assets/images/done.svg')
            }
            return path;
        }
    }
}
</script>

<style lang="scss" scoped>
    .items{
        li{
            border: 1px solid #ccc;
            font-size:20px;
            height: 50px;
            line-height: 50px;
            span{
                margin-left: 20px;
            }
            .item-icon{
                float: left;
                margin-top:10px;
                margin-left: 5px;
                max-width: 30px;
                max-height: 30px;
                cursor: pointer;
            }
            .item-remove{
                float:right;
                max-width: 24px;
                margin-top: 13px;
                margin-right: 10px;
                display: none;
                cursor: pointer;
            }
        }
        li:hover{
            .item-remove{
               display:block; 
            }
        }
    }
</style>



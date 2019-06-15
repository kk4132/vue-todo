<template>
    <section id="todo">
        <input type="text" 
                placeholder="接下去做什么?" 
                @keyup.enter="addItem"
                class="item-input"
                v-model="todoMsg"
        />
        <items 
            :itemData="disData"
            @changState="changState($event)"
            @remove="itemData.splice($event,1)"
        ></items>
        <div class="todo-footer">
            <span>{{disData.length}} items left</span>
            <tabs @switchTab="currTab = $event"></tabs>
            <span @click="removeCompleted">Clear Completed</span>
        </div>
    </section>
</template>

<script>
import items from '../components/items'
import tabs from '../components/tabs'
export default {
    data(){
        return{
            itemData:[],
            nextId:2,
            todoMsg:'',
            currTab:'all'
        }
    },
    computed:{
        disData(){
            let tab = this.currTab,
                items = this.itemData;
            if(tab === 'all'){
                return items
            }else{
                return items.filter(function(item){
                    return item.state === tab
                })
            }
        }
    },
    methods:{
        addItem(){
            let content = this.todoMsg;
            let result = /\S+/.test(content);
            if(result){
                let item = {
                    id:this.nextId++,
                    content,
                    state:'active'
                }
                this.itemData.unshift(item);
                this.todoMsg = ''
            }
        },
        changState(args){
            let [id,state] = [...args];
            this.itemData.forEach(function(item){
                if(item.id === id){
                    item.state = state;
                }
            })
        },
        removeCompleted(){
            this.itemData = this.itemData.filter((item)=>{
                if(item.state !== 'completed')return true;
            })
        }
    },
    components:{
        items,
        tabs
    }
}
</script>

<style lang="scss" scoped>
    #todo{
        border: 1px solid #ccc;
        border-radius: 5px;
        color: #fff;
        .item-input{
            color: #666;
        }
        .todo-footer{
            height: 30px;
            line-height: 30px;
            overflow: hidden;
            box-sizing: border-box;
            padding:0 10px; 
            &>*{
                float: left;
                box-sizing: border-box;
            }
            &>*:nth-child(1){
                width: 25%;
                display: inline-block;
            }
            &>*:nth-child(2){
                width: 50%;
            }
            &>*:nth-child(3){
                width: 25%;
                text-align: right;
            }
        }
    }
</style>


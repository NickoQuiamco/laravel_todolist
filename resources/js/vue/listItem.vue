<template>
    <div class="item">
        <input type="checkbox" @change="updateCheck()" v-model="item.completed" />
       <span :class="[item.completed ? 'completed' : '', 'item-text']" >{{ item.name }}</span>
       <button @click="removeItem()" class="trash-can" >
           <font-awesome-icon icon="trash" ></font-awesome-icon>
       </button>
    </div>
</template>

<script>
export default {
    props:['item'],
    methods:{
        updateCheck(){
            axios.put('/api/item/'+ this.item.id, {item: this.item } ).then(resp=>{
                // if(resp.status == 200) this.$emit('itemChanged');
                // console.log(resp);
            }).catch(err=>{
                console.log(err);
            })
        },
        removeItem(){
            axios.delete('/api/item/' + this.item.id).then(resp=>{
                console.log(resp);
                if(resp.status == 200){
                    this.$emit('itemChanged');
                }
            }).catch(err=>{
                console.log(err);
            })
        }
    }
}
</script>

<style scoped>
    .completed{
        text-decoration: line-through;
        color: #999;
    }
    .item-text{
        width: 100%;
        margin-left: 22px;

    }
    .item{
        display:flex;
        justify-content: center;
        align-items: center;
    }
    .trash-can{
        background: #e5e5e5;
        cursor: pointer;
        border: none;
        color: red;
        padding: 5px;
        margin: 5px;
        outline: none;
    }
</style>
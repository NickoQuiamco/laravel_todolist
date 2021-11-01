<template>
  <div class="todoListContainer">
      <div class="heading">
            <h2 id="title">
                Todo List
            </h2>
            <add-item-form @itemChanged="getList()" />
      </div>
      <listView :items="items" @itemChanged="getList()" />
  </div>
</template>
<script>
import addItemForm from './addItemForm';
import listView from './listView';
export default {
    components:{
        addItemForm,
        listView
    },
    data(){
        return{
            items: [] 
        }
    },
    methods:{
        getList(){
            axios.get('/api/items').then(resp=>{
                this.items = resp.data
            }).catch(err=>{
                console.log(err);
            })
        }
    },
    created(){
        this.getList();
    }
}
</script>
<style scoped>
.todoListContainer{
    width:600px;
    margin: auto;
}
.heading{
    background: #e6e6e6;
    padding: 13px;
}
#title{
    text-align: center;
}
</style>
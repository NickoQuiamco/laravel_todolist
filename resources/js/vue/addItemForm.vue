<template>
    <div class="addItem">
        <input v-model="item.name" type="text"  @keyup.enter="addItem()" />
        <font-awesome-icon
            @click="addItem()"
            :class="[ item.name ? 'active' : 'inactive', 'plus' ]"
            icon="plus-square" />
    </div>
</template>

<script>
export default {
    data(){
        return{
            item: {
                name: ""
            }
        }
    },
    methods:{
        addItem(){
            // console.log(this.item.name);
            if(this.item.name == ""){
                alert("Invalid input");
                return
            }

            axios.post('api/item/store',{ item: this.item }).then(response=>{
                // console.log(response);
                if(response.status == 201){
                    this.item.name = ""
                    this.$emit('itemChanged');
                }
            }).catch(err=>{
                console.log(err);
            });
        }
    }
}
</script>
<style scoped>
.addItem{
    display: flex;
    justify-content: center;
    align-items: center;
}
input{
    background: #f7f7f7;
    border: 0px;
    outline: none;
    padding: 5px;
    margin-right: 5px ;
    width: 100% ;
}
.plus{
    font-size: 22px;
    cursor: pointer;
}
.active{
    color: #00CE25;
}
.inactive{
    color: #999;
}
</style>
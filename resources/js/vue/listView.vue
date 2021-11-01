<template>
    <div>
        <div v-for="(item, index) in items" :key="index" >
            <list-item :item="item" class="item" @itemChanged="$emit('itemChanged')" ></list-item>
        </div>
    </div>
</template>

<script>
import listItem from './listItem.vue';
export default {
    props:['items'],
    components: {
        listItem
    }
}
</script>
<style scoped>
    .item{
        background: #e6e6e6;
        padding: 5px;
        margin-top: 3px;
    }
</style>
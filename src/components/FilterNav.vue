<template>
   <nav class="filter-nav">
        <ul>
            <li @click="filterBy('all')" :class="{active: current === 'all'}">All</li>
            <li @click="filterBy('complete')" :class="{active: current === 'complete'}">Complete</li>
            <li @click="filterBy('ongoing')" :class="{active: current === 'ongoing'}">Ongoing</li>
        </ul>
   </nav>
</template>

<script>
export default {
    props:['current'],

    methods:{
        filterBy(value){
            // console.log(value)
            this.$emit('filterValue',value);
        }
    }
}
</script>

<style>

ul li{
    list-style: none;
    display: inline-block;
    padding: 0 12px;
    margin: 0 12px;
    font-size: 14px;
    font-weight: bold;
    text-transform: uppercase;
    color: #999;
    letter-spacing: 1px;
    cursor: pointer;
}

.active{
    color: #333;
}
</style>
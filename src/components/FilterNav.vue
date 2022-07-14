<template>
  <nav class="filterNav">
    <button @click="filterBy('all')" :class="{active : current==='all'}">All</button>
    <button @click="filterBy('complete')" :class="{active : current ==='complete'}">Complete</button>
    <button @click="filterBy('ongoing')" :class="{active : current==='ongoing'}">Ongoing</button>
  </nav>
</template>

<script>
export default {
    props:['current'],
    methods:{
        filterBy(value){
            this.$emit("currentNav",value);
        }
    }
}
</script>

<style>
.filterNav button{ 
    border: none;
    background: none;
    color: #bbb;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    font-weight: bold;
    letter-spacing: 1px;
    cursor: pointer;
}
button.active{
    color: #333;
}
</style>
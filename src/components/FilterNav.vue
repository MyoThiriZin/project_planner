<template>
    <nav class="filter-nav">
        <button @click="filterBy('All')" :class="{ active : current==='All' }">All</button>
        <button @click="filterBy('Ongoing')" :class="{ active : current==='Ongoing' }">Ongoing</button>
        <button @click="filterBy('Complete')" :class="{ active : current==='Complete' }">Complete</button>
    </nav>
</template>

<script>
export default {
    data(){
        return{
            
        }
    },
    props:['current'],
    methods:{
        filterBy(value){
            this.$emit("filterValue",value)
        }
    }
}
</script>

<style>
    .filter-nav button {
        border: none;
        background: none;
    }
    button.active {
        color: red;
    }
</style>
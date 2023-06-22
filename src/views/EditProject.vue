<template>
    <h1>Edit {{id}}</h1>
    <form @submit.prevent="editProject">
    <label>Project Title</label>
    <input type="text" v-model="title">
    <label>Project Detail</label>
    <input type="text" v-model="detail">
    <button @click="updateProject">Update Project</button>
  </form>
</template>

<script>
export default {
    props:["id"],
    data(){
        return{
            title:"",
            detail:"",
        }
    },
    mounted(){
        fetch('http://localhost:3000/projects/'+this.id)
        .then((res)=>{
            return res.json()
        })
        .then((datas)=>{
            this.detail=datas.detail;
            this.title=datas.title;
        })
        .catch((err)=>{
            console.log(err)
        })
    },
    methods:{
        updateProject(){
            fetch('http://localhost:3000/projects/'+this.id, {
                method:"PATCH",
                headers:{
                    "Content-type":"application/json"
                },
                body:JSON.stringify({
                    title:this.title,
                    detail:this.detail
                })
            })
            .then(()=>{
                this.$router.push({name:"home"})
            })
            .catch((err)=>{
                console.log(err)
            })
        }
    }
}
</script>

<style scoped>
label {
    display: block;
}
input {
    width: 100%;
    padding: 10px 5px;
    border: none;
    border-bottom: 1px solid #ddd;
    margin-bottom: 20px;
}
button {
    display: block;
    margin: 0 auto;
    padding: 10px 20px;
    background-color: palevioletred;
    color: #fff;
    border: none;
    cursor: pointer;
    border-radius: 5px;
}
</style>
<template>
  <h1>Add Project</h1>
  <form @submit.prevent="addProject">
    <label>Project Title</label>
    <input type="text" v-model="title">
    <label>Project Detail</label>
    <input type="text" v-model="detail">
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  data(){
    return{
      title:"",
      detail:"",
    }
  },
  methods:{
    addProject(){
      fetch('http://localhost:3000/projects',
      {
        method:"POST",
        headers:{
          "Content-type":"application/json",
        },
        body:JSON.stringify({
          title:this.title,
          detail:this.detail,
          complete:false,
        })
      })
      .then(()=>{
        // redirect
        this.$router.push("/");
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
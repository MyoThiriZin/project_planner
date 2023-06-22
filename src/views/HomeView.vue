<template>
  <div class="home">
    <h1>Home</h1>
    <FilterNav @filterValue="current=$event" :current="current"></FilterNav>
    <div v-for="project in filteredProjects" :key="project.id">
      <SingleProject :project="project" @delete="deleteProject" @complete="completeProject"></SingleProject>
    </div>
    {{current}}
  </div>
</template>

<script>


import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'
export default {
  name: 'HomeView',
  components: {
    FilterNav,
    SingleProject,
  },
  data(){
    return {
      projects:[],
      current:"All"
    }
  },
  computed: {
    filteredProjects(){
      if(this.current==="Complete"){
        return this.projects.filter((p)=>{
          return p.complete;
        })
      }
      if(this.current==="Ongoing"){
        return this.projects.filter((p)=>{
          return !p.complete;
        })
      }
      return this.projects;
    }
  },
  methods: {
    deleteProject(id){
      this.projects=this.projects.filter(project=>{
        return project.id!=id;
      });
    },
    completeProject(id){
      let findProject=this.projects.find(project=>{
        return project.id===id;
      });
      findProject.complete=!findProject.complete;
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then((response)=>{
      return response.json();
    })
    .then((datas)=>{
      this.projects=datas;
    })
    .catch((err)=>{
      console.log(err)
    })
  }
}
</script>

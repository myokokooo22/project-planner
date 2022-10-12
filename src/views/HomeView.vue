<template>
  <div class="home">
    <h1>Home</h1>
    <FilterNav @filterValue="current = $event" :current = "current"/>

    <div v-for="project in filteredProjects" :key="project.id">
       <SingleProject :project="project"  @delete="deleteProject" @complete="completeProject"></SingleProject>
    </div>
  </div>

  {{current}}
</template>

<script>

import SingleProject from "../components/SingleProject";
import FilterNav from "../components/FilterNav";

export default {
  name: 'HomeView',
  components: {
   SingleProject,FilterNav
  },

  data(){
    return{
      projects: [],
      current: "all",
    }
  },
  
  computed:{
    filteredProjects(){
      if(this.current === 'complete'){
        return this.projects.filter((project)=>{
          return project.complete
        })
      }
      if(this.current === 'ongoing'){
        return this.projects.filter((project)=>{
          return !project.complete
        })
      }
      return this.projects;
    }
  },

  methods:{
    deleteProject(id){
      this.projects = this.projects.filter(project => {
          return project.id !== id;
      })
    },

    completeProject(id){
       let findProject = this.projects.find(project => {
          return project.id === id;
       })
       findProject.complete =!findProject.complete;
    }
  },

  mounted(){
    fetch("http://localhost:3000/projects")
    .then((response)=>{
      return response.json();
    })
    .then((datas)=>{
      this.projects = datas
    })
    .catch((err)=>{
      console.log(err.message());
    })
  }
}
</script>

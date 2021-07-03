<template>
  <div class="container" style="display:block;margin:20px 40px;">
    <title>Projects: {{cache.name}}</title>
      <center> <h1>Projects</h1> </center>
      <br/><br/>
    <div class="projects">
         <div v-for="project in cache.projects" :key="project.key" class="project">
      <div class="head">
          <div class="title">{{project.name}}</div>
       <div class="languages">
         <img class="lang" :src="getImage(lang)" :key="lang.key" v-for="lang in project.flags" />
                </div>
      </div>
        <div class="description"> {{project.description}} </div>
      </div>
     </div>
  </div>
  </template>
  
  <script>
  import conf from "../config/5.json";
    export default{
      name:'Projects',
      data(){
        return{
         cache:conf
        }
      },
      methods:{
        getImage(i){
           return require('../assets/images/'+i+'.png')
        }
      }
    }
  </script>
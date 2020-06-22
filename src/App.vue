<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <createProject v-on:add-project="addProject"/>
    <hr>
    <view-list :projects='result'/>

    {{result}}
  </div>
</template>

<script>
import axios from 'axios'
import viewList from './components/viewList'
import createProject from './components/createProject'

export default {
  name: 'App',
  components: {
   viewList,
   createProject
  },

  data(){
    return{
        result: null
    }
  },

  created() {
    this.getData();
  },

  methods: {
    getData(){
        axios.get('db.json')
        .then(res => {
      this.result = res.data._embedded.projects
     
      })
      .catch(error => console.log(error));
    },

    addProject(toAdd){
     
    axios.post('db.json', toAdd)
    .then(res=>  this.result = [...this.result, res.data._embedded.projects])
    .catch(err=>console.log(err))
    }
  },

  
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
 
}
</style>

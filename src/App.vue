<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <createProject  @addProject="result = addData"/>
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
        axios.get('backendData.json')
        .then(res => {
      this.result = res.data._embedded.projects
      // console.log(res.data.consolidated_weather[0])
      // console.log(this.result)
      })
      .catch(error => console.log(error));
    }
  },

  addData(){
    this.result.push({
      name: 'MOFO',
      status: 'DELIVERED'
    })
  }
  
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

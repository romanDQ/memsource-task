<template>
  <div>
    <createProject v-on:add-project="addProject" />
    <hr />
    <view-list :projects="result" />
  </div>
</template>

<script>
import axios from "axios";
import viewList from "./viewList";
import createProject from "./createProject";

export default {
  components: {
    viewList,
    createProject
  },

  data() {
    return {
      result: null
    };
  },

  created() {
    this.getData();
  },

  methods: {
    getData() {
      axios
        .get(
          "https://cors-anywhere.herokuapp.com/https://my-json-server.typicode.com/romanDQ/data/_embedded"
        )
        .then(res => {
          this.result = res.data.projects;
        })
        .catch(error => console.log(error));
    },

    addProject(newProject) {
      // const {name, status, id} = newProject
      this.result = [...this.result, newProject];

      // axios.post('https://cors-anywhere.herokuapp.com/https://my-json-server.typicode.com/romanDQ/data/_embedded', {
      //   name,
      //   status,
      //   id
      // })
      // .then(res=>  this.result = [...this.result, res.data.projects])
      // .catch(err=>console.log(err))
    }
  }
};
</script>
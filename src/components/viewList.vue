<template>
  <div class="viewList">
    <h2>Project List:</h2>
    <button @click="sortName">Sort by Name</button>
    <button @click="sortID">Sort by ID</button>
   
    <div>
      <button
        :class="{active: filter =='filterByName'}"
        @click="filter = 'filterByName'"
      >Filter by Name</button>
      <button
        :class="{active: filter =='filterByStatus'}"
        @click="filter = 'filterByStatus'"
      >Filter by Status</button>
    </div>
    <input v-model="search" />
    <ul>
      <li v-for="list in filteredList" :key="list.id">
        <projectList v-bind:list="list"/>
        <hr />
      </li>
    </ul>
  </div>
</template>

<script>
import projectList from "./projectList";

export default {
 
  props: ["projects"],

  data() {
    return {
      filter: '',
      search: ''
    };
  },

  components: {
    projectList
  },

  methods: {
    sortName() {
      this.projects.sort((a, b) => {
        var nameA = a.name.toLowerCase(),
          nameB = b.name.toLowerCase();
        if (nameA < nameB)
         
          return -1;
        if (nameA > nameB) return 1;
        return 0; 
      });
    },
    sortID() {
      this.projects.sort((a, b) => {
        return a.id - b.id;
      });
    },
  },

  computed: {
    filteredList() {
      if (this.filter == "filterByName") {
        return this.projects.filter(el => {
          return el.name.toLowerCase().includes(this.search.toLowerCase());
        });
      } else if (this.filter == "filterByStatus") {
        return this.projects.filter(el => {
          return el.status.toLowerCase().includes(this.search.toLowerCase());
        });
      }

      return this.projects;
    }
  }
};
</script>

<style>
.viewList{
    text-align: center;
}
</style>
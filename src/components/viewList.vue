<template>
  <div class="viewList">
    <h2>Project List:</h2>
    
    <button class="btn btn-primary" style="margin-right: 10px;" @click="sortName">Sort by Name</button>
    <button class="btn btn-primary" style="margin-right: 10px;" @click="sortID">Sort by ID</button>
    <button class="btn btn-primary" style="margin-right: 10px;" @click="sortStatus">Sort by Status</button>
    <button class="btn btn-primary" style="margin-right: 10px;" @click="sortDate">Sort by Date</button>

    <div class="filter-container">
      <b-button pill variant="outline-secondary"
        style="margin-right: 10px;"
        :class="{active: filter =='filterByName'}"
        @click="filter = 'filterByName'"
      >
      Filter by Name
      </b-button>

      <b-button pill style="margin-right: 10px;"
        variant="outline-secondary"
        :class="{active: filter =='filterByStatus'}"
        @click="filter = 'filterByStatus'"
      >
      Filter by Status
      </b-button>

      <div class="filter-input">
        <b-form-input v-model="search" placeholder="search with filter:"></b-form-input>
      </div>
    </div>

    <div class="project-list">
      <ul>
        <li v-for="list in filteredList" :key="list.id">
          <projectList v-bind:list="list" />
          <hr />
        </li>
        <div></div>
      </ul>
    </div>
  </div>
</template>

<script>
import projectList from "./projectList";

export default {
  props: ["projects"],

  data() {
    return {
      filter: "",
      search: "",
    };
  },

  components: {
    projectList
  },

  methods: {
    sortName() {
      this.projects.sort((a, b) => {
        let firstName = a.name.toLowerCase(),
          secondName = b.name.toLowerCase();
        if (firstName < secondName) return -1;
        if (firstName > secondName) return 1;
        return 0;
      });
    },
    sortID() {
      this.projects.sort((a, b) => {
        return a.id - b.id;
      });
    },

    sortStatus() {
      this.projects.sort((a, b) => {
        let firstStatus = a.status.toLowerCase(),
          secondStatus = b.status.toLowerCase();
        if (secondStatus < firstStatus) return -1;
        if (secondStatus > firstStatus) return 1;
        return 0;
      });
    },

    sortDate() {
      this.projects.sort((a, b) => {
        let firstDate = new Date(a.dateDue),
          secondDate = new Date(b.dateDue);
        return secondDate - firstDate;
      });
    }
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
    },
  }
};
</script>

<style>
.viewList {
  display: block;
  text-align: center;
  margin: 25px 300px 75px 300px;
}

.project-list {
  display: block;
  margin: 75px 75px 75px 100px;
  color: black;
}

.filter-container {
  padding: 20px;
}

.filter-input {
  margin: 15px;
}
</style>
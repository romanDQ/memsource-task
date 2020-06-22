<template>
  <div class="container">
    <b-card bg-variant="light">
      <b-form-group
        label-cols-lg="3"
        label="Create/Edit Project"
        label-size="lg"
        label-class="font-weight-bold pt-0"
        class="mb-0"
      >
        <b-form-group
          label-cols-sm="3"
          label="Name:"
          v-model="name"
          label-align-sm="right"
          label-for="nested-name"
        >
          <b-form-input v-model="name" id="nested-name"></b-form-input>
        </b-form-group>

        <b-form-group label-cols-sm="3" label="Target language:" label-align-sm="right">
          <b-form-checkbox-group
            id="checkbox-group-1"
            v-model="targetLanguage"
            :options="optionsLanguage"
          ></b-form-checkbox-group>
        </b-form-group>

        <b-form-group
          label-cols-sm="3"
          label="Source language:"
          label-align-sm="right"
          class="mb-0"
        >
          <b-form-group>
            <b-form-radio v-model="srcLanguage" name="english" value="en">en</b-form-radio>
            <b-form-radio v-model="srcLanguage" name="czech" value="cz">cs</b-form-radio>
            <b-form-radio v-model="srcLanguage" name="japan" value="ja">ja</b-form-radio>
          </b-form-group>

        </b-form-group>

        <b-form-group label-cols-sm="3" label="Status:" label-align-sm="right" class="mb-0">
          <b-form-select v-model="selectedStatus" :options="optionsStatus"></b-form-select>
        </b-form-group>

        <b-form-group label-cols-sm="3" label-align-sm="middle" class="mb-0">
          <div class="create-project-btn" v-if="!isSubmited">
            <button class="btn btn-primary" @click.prevent="projectCreate">Create Project</button>
          </div>
        </b-form-group>

      </b-form-group>
    </b-card>

    <div class="project-detail" v-if="isSubmited" >
      <b-alert show variant="warning">Edit, or Add Project</b-alert>
      <b-list-group v-if="isSubmited">
        <h2>Project details:</h2>
        <b-list-group-item>Id:{{id}}</b-list-group-item>
        <b-list-group-item>status:{{selectedStatus}}</b-list-group-item>
        <b-list-group-item>source language: {{srcLanguage}}</b-list-group-item>
        <b-list-group-item>target langugages: {{targetLanguage}}</b-list-group-item>

        <div class="btn-add-Project">
          <b-button block variant="primary" @click="addToList">Add Project to List</b-button>
        </div>

      </b-list-group>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isSubmited: false,
      isEditing: false,
      id: 11,
      name: "",
      targetLanguage: [],
      selectedStatus: [],
      srcLanguage: [],
      optionsLanguage: [
        { text: "cs", value: "cs" },
        { text: "en", value: "en" },
        { text: "ja", value: "ja" },
        { text: "la", value: "la" }
      ],
      optionsStatus: [
        { value: [], text: "Please select an option" },
        { value: "PROCESSING", text: "Processing" },
        { value: "DELIVERED", text: "Delivered" }
      ]
    };
  },

  methods: {
    projectCreate() {
        if((this.name.length == 0) || (this.srcLanguage.length == 0) || (this.targetLanguage.length == 0) || (this.selectedStatus.length == 0) ){
            alert('Enter all values in the Create/Edit fields before proceeding.')
        }else{
             this.isSubmited = true;
        }
    },

    addToList(event) {
      event.preventDefault();
     
        let newProject = {
        name: this.name,
        sourceLanguage: this.srcLanguage,
        targetLanguages: this.targetLanguage,
        id: this.id,
        status: this.selectedStatus
      };

      this.$emit("add-project", newProject);
      this.id++;
      this.clearFields();
    },

    clearFields() {
      this.name = "";
      this.targetLanguage = [];
      this.srcLanguage = [];
      this.selectedStatus = [];
      this.isSubmited = false;
    }
  }
};
</script>

<style >
h2 {
  text-align: center;
}

.container {
  margin: 25px 50px 75px 100px;
}

.project-detail {
  text-align: center;
  padding: 20px;
}

.btn-add-Project {
  padding: 20px;
  text-align: center;
}

.create-project-btn {
  padding: 20px;
}
</style>
<template>
  <section>
    <div>
      <b-list-group>
        <b-list-group-item class="name">name: {{list.name}}</b-list-group-item>
        <b-list-group-item>id: {{list.id}}</b-list-group-item>
        <b-list-group-item>status: {{list.status}}</b-list-group-item>
        <b-list-group-item>due date: {{list.dateDue}}</b-list-group-item>
        <b-list-group-item>source language: {{list.sourceLanguage}}</b-list-group-item>
        <b-list-group-item>target languages: {{list.targetLanguages}}</b-list-group-item>
      </b-list-group>
    </div>
  </section>
</template>

<script>
export default {
  name: "projectList",
  props: ["list"]
};
</script>

<style>
.name {
  font-size: 20px;
  font-family: Georgia, "Times New Roman", Times, serif;
  text-emphasis: bold;
}
</style>
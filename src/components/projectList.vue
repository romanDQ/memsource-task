<template>
<section>
  
     <div>
      <p>name: {{list.name}}</p>
      <p>id: {{list.id}}</p>
      <p>status: {{list.status}}</p>
      <p>due date: {{list.dateDue}}</p>
      <p>languages: {{list.targetLanguages}}</p>
  </div>
</section>
 
</template>

<script>
export default {
    name: 'projectList',
    props: [
        "list"
    ],
}
</script>
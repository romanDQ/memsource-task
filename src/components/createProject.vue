<template>
    <div>
         <h2>hello</h2>
         <input type="text" v-model="toAdd.name">Name:
         <input type="text" v-model="toAdd.status">Status:
         <input type="text" v-model="toAdd.sourceLanguage">Source:
         <input type="text" v-model="toAdd.targetLanguage">Target:
         {{toAdd.name}}
        <button @click="$emit('add-project', toAdd)">Add Projects</button>

        
    </div>
    
    
</template>

<script>
export default {
    data(){
        return{
            toAdd: {
                name: '',
                status: '',
                sourceLanguage: '',
                targetLanguage: ['']
            }
        }
    },

    methods:{
        
    }

    
}
</script>
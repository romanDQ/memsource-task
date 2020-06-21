<template>
    <div>
         <h2>hello</h2>
        <button @click="addData">Add Projects</button>
    </div>
    
</template>

<script>
export default {
   

    data(){
        return{
            toAdd: {
                name: 'MOFO',
                status: 'DELIVERED'
            }
        }
    },

    props:[],

    methods:{
        addData(event){
            this.$emit('addProject')
            console.log(this.toAdd)
        }
    }
}
</script>
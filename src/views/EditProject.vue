<template>
  <h1>Edit project</h1>
  <form @submit.prevent="UpdateHandler">
    <label>Title</label>
    <input v-model="title" type="text" required />
    <label>Details:</label>
    <textarea v-model="details" required></textarea>
    <button>Update project</button>
  </form>
</template>

<script>

export default {
    props:['id'],
    data(){
        return{
            title:"",
            details:"",
            uri: "http://localhost:3000/projects/" + this.id
        }
    },
    mounted(){
        fetch(this.uri)
        .then(res => res.json())
        .then(data => {
            
            this.title = data.title
            this.details = data.details
        })
    },
    methods:{
    UpdateHandler(){ 
        let project = {
            title: this.title,
            details:this.details
        }
        fetch(this.uri,{
            method: 'PATCH',
                headers: {'Content-type': 'application/json'},
                body: JSON.stringify(project)
                }).then(()=>{
                    this.$router.push('/')
                }).catch((err) => console.log(err))
    

         
    }
    }

}
</script>

<style>
</style>
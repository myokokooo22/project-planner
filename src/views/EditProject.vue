<template>
    <h1>Edit Project</h1>

    <form @submit.prevent="addProject">
        <label>Project Title: </label>
        <input type="text" v-model="title"/>

        <label>Project Details: </label>
        <input type="text" v-model="details"/>

        <button type="submit" @click="updateProject">Update</button>
    </form>
</template>

<script>
export default {
    props:['id'],

    data(){
        return{
            title:"",
            details: "",
        }
    },

    methods:{
        updateProject(){
            fetch("http://localhost:3000/projects/" + this.id, {
                method: 'PATCH',
                headers:{
                    "Content-type":"application/json"
                },
                body:JSON.stringify({
                    title: this.title,
                    details: this.details
                })              
            })
            .then(()=>{
                this.$router.push("/")
             })
             .catch((err)=>{
                console.log(err)
             })
        }
    },  

    mounted(){
        fetch("http://localhost:3000/projects/" + this.id)
        .then((response)=>{
            return response.json();
        })
        .then((data)=>{
            this.title = data.title;
            this.details = data.details
        })
        .catch((err)=>{
            console.log(err);
        })
    }
}
</script>

<style>

</style>
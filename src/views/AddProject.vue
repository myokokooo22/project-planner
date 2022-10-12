<template>
    <h1>Add Project</h1>
    <form @submit.prevent="addProject">
        <label>Project Title: </label>
        <input type="text" v-model="title"/>

        <label>Project Details: </label>
        <input type="text" v-model="details"/>

        <button type="submit">Add Project</button>
    </form>
</template>

<script>
export default {
    data(){
        return{
            title: "",
            details: ""
        }
    },

    methods:{
        addProject(){
            fetch('http://localhost:3000/projects',  
                {
                    method: "POST",
                    headers:{
                        "Content-Type": "application/json"
                    },
                    body:JSON.stringify(
                        {
                            title: this.title,
                            details: this.details,
                            complete: false
                        }
                    )
                }
            )
           .then(()=>{
                //redirect 
                // this.$router.push({name: 'home'})
                this.$router.push("/")
           })
           .catch((err)=>{
                console.log(err)
           })
        }
    }
}
</script>

<style>
    *{
        box-sizing: border-box;
    }

    form{
        background: #fff;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 5px 5px rgba(0,0,0,0.3), 
        0 -3px 5px rgba(0,0,0,0.3);
    }

    label{
        display: block;
        color: #999;
        text-transform: uppercase;
        font-size: 14px;
        font-weight: bold;
        letter-spacing: 1px;
        margin: 20px 0 10px 0;
    }

    input{
        padding: 10px;
        border: 0;
        border-bottom: 2px solid #999;
        width: 100%;
        background: none;
    }

    input:focus{
        outline: 0;
    }

    button{
        display: block;
        padding: 20px 30px;
        background: seagreen;
        color: white;
        font-size: 16px;
        border: 0;
        border-radius: 10px;
        margin: 20px auto;
        cursor: pointer;
    }
</style>
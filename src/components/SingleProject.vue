<template>
   <div class="project" :class="{complete:project.complete}">
       <div class="flex">
            <div @click="showDetail = !showDetail"><h4>{{project.title}}</h4></div>
            <div>
                <span class="material-icons" @click="deleteProject">delete</span>
                
                <router-link :to="{name: 'editproject', params:{id: project.id} }">
                    <span class="material-icons">edit</span>
                </router-link>

                <span class="material-icons" @click="completeProject">check</span>
            </div>
        </div> 
        <p v-if="showDetail">Details: {{project.details}}</p>  
   </div>
</template>

<script>
export default {
    props:['project'],

    data(){
        return{
            api: "http://localhost:3000/projects/",
            showDetail: false
        }
    },

    methods:{
        deleteProject(){
            let deleteRoute = this.api + this.project.id;
            fetch(deleteRoute, {method:"DELETE"}) 
            // console.log(this.api + this.project.id, {method:"DELETE"})
            .then(()=>{
                this.$emit("delete",this.project.id)
            })

            .catch((err)=>{
                console.log(err)
            })
        },

        completeProject(){
            let updateCompleteRoute = this.api + this.project.id;
            // console.log(updateCompleteRoute)
            fetch(updateCompleteRoute, {
                method: "PATCH",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(
                    {
                        complete: !this.project.complete
                    }
                )
            })
            .then(()=>{
                this.$emit("complete",this.project.id)
            })

            .catch((err)=>{
                console.log(err);
            })
        }
    }
}
</script>

<style>
    .project{
        padding: 20px;
        background: #f4f4f4;
        margin: 12px;
        box-shadow: 0 3px 5px rgba(0,0,0,0.4);
        border-left: 6px solid crimson;
        border-radius: 10px;
    }

    h4{
        color: indigo;
        cursor: pointer;
    }

    .flex{
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    span{
        margin-left: 6px;
    }

    span:hover{
        color: #777;
        cursor: pointer;
    }

    .complete{
        border-left: 6px solid yellowgreen;;
    }
</style>
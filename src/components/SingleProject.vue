<template>
    <div class="projects" :class="{complete:project.complete}">
        <div class="flex">
            <div>
                <h3 @click="showDetail">{{project.title}}</h3>
                
            </div>
            <div>
                <span class="material-symbols-outlined" @click="deleteProject">
                    delete
                </span>
                <router-link :to="{name:'EditProject',params:{id:project.id} }">
                    <span class="material-symbols-outlined">
                    edit
                    </span>
                </router-link>
                <span class="material-symbols-outlined" @click="completeProject">
                    done
                </span>
            </div>
        </div>
        <p v-if="detail">{{project.detail}}</p>
        {{project.complete}}
    </div>
</template>

<script>
export default {
    props:['project'],
    data(){
        return{
            detail:false,
            api:'http://localhost:3000/projects',
            // complete:true,
        }
    },
    methods:{
        showDetail(){
            this.detail=!this.detail;
        },
        deleteProject(){
            let deleteRoute= this.api+"/"+this.project.id
            fetch(deleteRoute,{method:"DELETE"})
            .then(()=>{
                this.$emit("delete", this.project.id)
            })
        },
        completeProject(){
            let changeComplete = this.api+"/"+this.project.id;
            fetch(changeComplete,{
                method:"PATCH",
                headers:{
                    "Content-type":"application/json",
                },
                body:JSON.stringify(
                    {
                        complete:!this.project.complete
                    }
                )
            })
            .then(()=>{
                this.$emit("complete",this.project.id)
            })
            .catch((err)=>{
                console.log(err)
            })
        }
    }
}
</script>

<style>
    .projects {
        background-color: #eee;
        padding: 10px;
        margin: 20px 0;
        border-left: 6px solid crimson;
        border-radius: 5px;
    }
    .projects h3 {
        color: violet;
        cursor: pointer;
    }
    .flex {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .flex span {
        margin-right: 10px;
        cursor: pointer;
    }
    .flex span:last-child {
        margin-right: 0;
    }
    .complete {
        border-left: 6px solid greenyellow;
    }
</style>
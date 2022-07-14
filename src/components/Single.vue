<template>

  <div class="card" :class="{complete:project.complete}">
    <div class="title">
        <h3 @click="showDetail=!showDetail">{{project.title}}</h3>
        <div class="icons">
            <span class="material-icons delete" @click="deletePlan">delete</span>
            <router-link :to="{name:'EditPlan',params:{id:project.id}}">
                <span class="material-icons edit">edit</span>
            </router-link>
            <span class="material-icons done" @click="completePlan">done</span>
        </div>
        
    </div>

    <p v-if="showDetail">{{project.detail}}</p>

    <!-- {{project.complete}} -->
  </div>

</template>

<script>
export default {
    data(){
        return{
            showDetail: false,
            api: 'http://localhost:3000/projects',
        }
    },
    props:['project'],
    methods:{
        deletePlan(){
            let deleteRoute = this.api+"/"+this.project.id;

            fetch(deleteRoute,{method:"DELETE"})
            .then(()=>{
                this.$emit("delete",this.project.id)
            })
            .catch((err)=>{
                console.log(err.message);
            })
        },
        completePlan(){
            let completeRoute = this.api+"/"+this.project.id;
            fetch(completeRoute,{
                method: "PATCH",
                headers: {
                    "Content-Type":"application/json"
                },
                body: JSON.stringify(
                    {
                        complete : !this.project.complete
                    }
                )
            })
            .then(()=> this.$emit("complete",this.project.id))
            .catch((err)=> console.log(err.message))
        }
    }
}
</script>

<style>
.card{
    background-color: #f2f2f2;
    margin: 10px;
    padding: 15px;
    border-radius: 10px;
    border-left: 5px solid #c03546;
}
.title{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
h3{
    color: #3f3fa4;
    cursor: pointer;
}
.icons span{
    cursor: pointer;
    margin-right: 10px;
}
.icons span:hover{
    color: #777777;
}
.delete{
    color: #fc5185;
}
.edit{
    color: #e0c45c;
}
.done{
 color: #17b978;
}
p{
    color: #948c8c;
}
.complete{
    border-left-color: #74f9ff;
}
</style>
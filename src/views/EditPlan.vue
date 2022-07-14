<template>
  <h1>Edit</h1>
   <form @submit.prevent="addPlan">
        <label>Project title</label>
        <input type="text" v-model="title">
        <label>Project detail</label>
        <input type="text" v-model="detail">
        <button @click="editPlan">Edit Plan</button>
    </form>
</template>

<script>
export default {
    data(){
        return{
            title:'',
            detail:''
        }
    },
    props:['id'],
    mounted(){
        fetch('http://localhost:3000/projects/'+this.id)
        .then((res)=>{
            return res.json()
        })
        .then((data)=>{
            this.title = data.title;
            this.detail = data.detail;
        })
        .catch((err)=>{
            console.log(err.message);
        })
    },
    methods:{
        editPlan(){
            fetch("http://localhost:3000/projects/"+this.id,
            {
                method:"PATCH",
                headers:{
                    "Content-Type": "application/json"
                },
                body:JSON.stringify({
                    title: this.title,
                    detail: this.detail
                })
            })
            .then(()=>this.$router.push("/"))
        }
    }
}
</script>

<style>

</style>
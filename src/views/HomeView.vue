<template>

  <div class="home">
    <h1>Home</h1>

    <FilterNav @currentNav="current=$event" :current="current"></FilterNav>

    <div v-for="project in filterProject" :key="project.id">
      <Single :project="project" @delete="del" @complete="completeUi"></Single>
    </div>
  </div>
  <!-- {{current}} -->

</template>

<script>
import FilterNav from '../components/FilterNav'
import Single from '../components/Single'
export default {
  components: {
    FilterNav,
     Single },
  name: 'HomeView',
  data(){
    return{
      projects:[] ,//[{...},{...}]
      current: 'all'
    }
  },
  computed:{
    filterProject(){
      if(this.current === 'complete'){
        return this.projects.filter((el)=>el.complete)
      }
      if(this.current === 'ongoing'){
        return this.projects.filter((el) => {
          return !el.complete
        })
      }
      return this.projects
    }
  },
  methods:{
    del(id){
      this.projects = this.projects.filter((el)=>{
        return el.id != id;
      });
    },
    completeUi(id){
      let findPlan = this.projects.find((el)=>{
        return el.id === id; //{...}
      });
      findPlan.complete = !findPlan.complete;
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then((response)=> response.json())
    .then((datas)=>{
      this.projects=datas;
    })
    .catch((err)=>{
      console.log(err.message);
    })
  }
}
</script>

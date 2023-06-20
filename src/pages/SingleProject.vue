<template>
  <div class="container">
    <!-- se lascio in return project: '', v-if non serve -->
    <div v-if="project">
     <div class="card text-center">
    <img :src="project.image" :alt="project.title" class="card-img-top">
    <h1 class="card-title">{{ project.title }}</h1>
    <p>{{ project.description }}</p>
    </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { store } from '../store';
  export default {
    name: 'SingleProject',
    data() {
      return {
        store,
        project: null,
      }
    },
    methods: {
      getProject() {
        axios.get(`${store.apiUrl}/projects/${this.$route.params.slug}`).then((res) => {
          console.log(res.data.results);
          this.project = res.data.results;
          if(res.data.success) {
            this.project = res.data.results;
          } else {
            this.$router.push({ name: 'not-found' })
          }
        })
      }
    },
    mounted() {
    // console.log(this.$router);
    // console.log(this.$route)
    this.getProject();
    }
  }
</script>

<style lang="scss" scoped>

</style>
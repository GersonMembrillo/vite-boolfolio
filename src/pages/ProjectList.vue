<template>
  <div>
    <div class="container">
      <h1>{{ title }}</h1>
      <div class="row">
        <ProjectCard v-for="(project, index) in projects" :key="project" :project="project" />
    </div>
    <nav aria-label="Page navigation example">
      <ul class="pagination">
          <li class="page-item"><button :class="{ 'page-link': true, 'disabled': currentPage === 1 }"
              @click="getData(currentPage - 1)">Previous</button></li>
              <li class="page-item" v-for="n in lastPage"><button
                            :class="{ 'page-link': true, 'active': currentPage === n }" @click="getData(n)">{{ n }}</button>
              </li>
              <li class="page-item"><button :class="{ 'page-link': true, 'disabled': currentPage === lastPage }"
              @click="getData(currentPage + 1)">Next</button></li>
          </ul>
        </nav>
    </div>
  </div>
</template>

<script>
import ProjectCard from '../components/ProjectCard.vue';
import axios from 'axios';
import { store } from '../store';
export default {
  'name': 'ProjectList',
  components: {
    ProjectCard
  },
  data() {
    return {
      title: 'Hello World!',
      projects: [],
      store,
      apiUrl: 'http://127.0.0.1:8000/api',
      // imgBasePath: 'http://127.0.0.1:8000/storage/',
      currentPage: 1,
      lastPage: null,

    }
  },
  methods: {
    getData(numPage) {
      axios.get(`${store.apiUrl}/projects`, {
        params: {
          'page': numPage
        }
      }).then((res) => {
        // console.log(res)
        this.projects = res.data.results.data
        this.currentPage = res.data.results.current_page;
        this.lastPage = res.data.results.last_page;

      })
    }
  },
  mounted() {
    this.getData()
  }
}
</script>

<style lang="scss" scoped>

</style>
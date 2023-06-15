<template>
  <div>
    <div class="container">
      <h1>{{ title }}</h1>
      <div class="row">
        <div class="col" v-for="(project, index) in projects" :key="project.id">

          <div class="card h-100">
            <!--QUESTA SOLO NEL CASO DI IMG NELLO STORAGE <img :src="imgBasePath + project.image" class="card-img-top" :alt="project.title"> -->
            <img :src="project.image" class="card-img-top" :alt="project.title">
            <div class="card-body">
              <p class="card-title text-uppercase fw-bolder">{{ project.title }}</p>
              <p class="card-text">{{ project.description }}</p>
                <!-- <h6>Type: {{ project.type }}</h6> -->
            </div>
          </div>
        </div>

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
import axios from 'axios';
export default {
  'name': 'ProjectList',
  data() {
    return {
      title: 'Hello World!',
      projects: [],
      apiURL: 'http://127.0.0.1:8000/api',
      imgBasePath: 'http://127.0.0.1:8000/storage/',
      currentPage: 1,
      lastPage: null,

    }
  },
  methods: {
    getData(numPage) {
      axios.get(`${this.apiURL}/projects`, {
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
    this.getData(1)
  }
}
</script>

<style lang="scss" scoped>

</style>
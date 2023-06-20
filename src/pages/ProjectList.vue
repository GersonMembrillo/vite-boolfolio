<template>
  <div>
    <div class="container">
      <h1>{{ title }}</h1>
      <div class="row">

        <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 mb-4" v-for="(project, index) in projects" :key="project.id">
                <div class="card h-100">
                  <!--QUESTA SOLO NEL CASO DI IMG NELLO STORAGE <img :src="imgBasePath + project.image" class="card-img-top" :alt="project.title"> -->
                  <img :src="project.image" class="card-img-top img-fluid" :alt="project.title">
                  <div class="card-body d-flex flex-column justify-content-between">
                      <div>
                    <p class="card-title text-uppercase fw-bolder">{{ project.title }}</p></div>
                      <div class="d-flex align-items-end flex-column flow-end">
                          <router-link :to="{ name: 'single-project', params: { slug: project.slug } }" class="btn btn-primary">Details</router-link>

                      </div>
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
import { store } from '../store';
export default {
  'name': 'ProjectList',
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
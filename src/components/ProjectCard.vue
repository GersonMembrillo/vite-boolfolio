<template>
  <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 mb-4">
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
</template>

<script>
import { store } from '../store';
export default {
  name: 'ProjectCard',
  props: ['project'],
  data() {
    return {
      store
    }
  },
}
</script>

<style lang="scss" scoped></style>
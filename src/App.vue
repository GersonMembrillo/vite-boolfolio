<template>
  <HeaderApp></HeaderApp>
  <main>
      <router-view>

    </router-view>
  </main>
  <h4>Sono il footer bitches!</h4>
</template>

<script>
import HeaderApp from './components/HeaderApp.vue';
export default {
  name: 'App',
  components: {
    HeaderApp
}
}
</script>

<style lang="scss" scoped>
</style>
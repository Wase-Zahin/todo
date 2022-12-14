<template>
  <Header></Header>
  <Main></Main>
  <Footer></Footer>
</template>

<script>
import Header from './components/layout/header-section.vue'
import Main from './components/layout/main-section.vue'
import Footer from './components/layout/footer-section.vue'

export default {
  name: 'App',
  components: {
    Header,
    Main,
    Footer
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>

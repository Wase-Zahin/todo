<template>
  <Header @toggle-menu="toggleMenu = !toggleMenu"></Header>
  <Main :computer-screen="computerScreen" :showMenu="toggleMenu"></Main>
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
  },

  data() {
    return {
      toggleMenu: false,
      computerScreen: true,
    }
  },
  created() {
    window.addEventListener("resize", this.resizeFn);
  },
  unmounted() {
    window.removeEventListener("resize", this.resizeFn);
  },
  methods: {
    resizeFn() {
      if (window.screen.width >= 620) {
        this.computerScreen = true; 
        this.toggleMenu = false;
      } else this.computerScreen = false;
    }
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

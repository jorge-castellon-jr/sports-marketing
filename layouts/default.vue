<template>
  <b-container fluid>
    <Header />
    <nuxt />
    <Footer />
  </b-container>
</template>

<script>
import Header from '~/components/Header.vue'
import Footer from '~/components/Footer.vue'

export default {
  components: {
    Header,
    Footer
  }
}
</script>

<style>
:root {
  font-size: 16px;
  word-spacing: 1px;
  box-sizing: border-box;
}

p,h1,h2,h3,h4,h5,h6,div,a {
  font-family: proxima-nova, sans-serif;
}

h1 {
  font-size: 45px;
  line-height: 1.1em;
  margin-bottom: 10px;
}
h2 {
  font-size: 28px;
  line-height: 1.18em;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}
</style>

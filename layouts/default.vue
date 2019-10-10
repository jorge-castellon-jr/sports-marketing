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

<style lang="scss">
:root {
  font-size: 16px;
  word-spacing: 1px;
  box-sizing: border-box;
}

p,h1,h2,h3,h4,h5,h6,div,a {
  font-family: proxima-nova, sans-serif;
}

h1 {
  font-size: 32px;
  line-height: 1.1em;
  margin-bottom: 10px;

  @media only screen and (min-width: 576px) {
    font-size: 45px;
  }
}
h2 {
  font-size: 21px;
  line-height: 1.18em;
  
  @media only screen and (min-width: 576px) {
    font-size: 28px;
  }
}
a {
  color: white;
}

img {
  max-width: 100%;
  flex-shrink: 0;
  align-self: center;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}
</style>

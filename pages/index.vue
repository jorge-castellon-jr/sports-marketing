<template>
  <b-row>
    <b-img class="th__hero-image" :src="`${home.hero_image}`"></b-img>
    <b-container class="th__content" :style="cssProps">
      <h1 class="th__cta-title">{{ home.cta }}</h1>
      <h2 class="th__cta-body">{{ home.cta_body }}</h2>
      <b-button class="th__cta-btn" variant="dark" :href="`tel:${phone}`">
        <phoneSVG />
        {{ formatPhoneNumber(phone) }}
      </b-button>
      <Block :blocks="home.blocks"/>
    </b-container>
  </b-row>
</template>

<script>
import homeJSON from '~/content/data/home.json'
import companyJSON from '~/content/data/company.json'
import phoneSVG from '~/components/PhoneSVG.vue'
import Blocks from '~/components/Blocks.vue'

export default {
  data () {
    return {
      home: homeJSON,
      company: companyJSON,
      phone: companyJSON.phone
    }
  },
  components: {
    phoneSVG,
    Blocks
  },
  computed: {
    cssProps () {
      return {
        '--primary-color': this.home.primary_color,
        '--primary-hover': this.LightenDarkenColor(this.home.primary_color, 30),
        '--phone': this.formatPhoneNumber(this.phone)
      }
    },
  },
  methods: {
    formatPhoneNumber(phoneNumberString) {
      var cleaned = ('' + phoneNumberString).replace(/\D/g, '')
      var match = cleaned.match(/^(\d{3})(\d{3})(\d{4})$/)
      console.log(phoneNumberString)

      if (match) {
        var formated = '(' + match[1] + ') ' + match[2] + '-' + match[3]
        console.log(formated)
        return formated
      }
      return null
    },
    LightenDarkenColor(col, amt) {
    
      var usePound = false;
  
      if (col[0] == "#") {
        col = col.slice(1);
        usePound = true;
      }
  
      var num = parseInt(col,16);
  
      var r = (num >> 16) + amt;
  
      if (r > 255) r = 255;
      else if  (r < 0) r = 0;
  
      var b = ((num >> 8) & 0x00FF) + amt;
  
      if (b > 255) b = 255;
      else if  (b < 0) b = 0;
  
      var g = (num & 0x0000FF) + amt;
  
      if (g > 255) g = 255;
      else if (g < 0) g = 0;
  
      return (usePound?"#":"") + (g | (b << 8) | (r << 16)).toString(16);
    
    }
  }
}
</script>

<style lang="scss" scoped>
$primary-color: var(--primary-color);
$primary-hover: var(--primary-hover);
$cta: #313131;

.th {
  &__hero-image {
    // margin: 0 0 40px;
    margin-bottom: 40px;
    max-width: 100%;
  }
  &__content {
    max-width: 480px;
    // margin: 0 auto;
  }
  &__cta {
    &-title {
      color: $cta;
    }
    &-body {
      color: $cta;
      margin-bottom: 24px;
    }
    &-btn {
      padding: 10px 24px;
      background-color: $primary-color;
      border-color: $primary-color;
      font-size: 20px;
      svg {
        width: 30px;
        height: 30px;
        margin-right: 10px;
        fill: white;
      }
      &:hover, &:active, &:focus {
        background-color: $primary-hover !important;
        border-color: $primary-hover !important;
      }
    }
  }
  &__body {
    margin: 150px 0;
  }
}
</style>

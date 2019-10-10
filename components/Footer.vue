<template>
    <b-row class="th__footer" :style="cssProps">
        <b-container>
            <p><strong>{{ company.company_name }}</strong></p>
            <p>{{ phone }}</p>
            <p v-if="company.email_">{{company.email}}</p>
            <p v-if="company.address_">{{company.address}}</p>
            <p>© {{ year() }}, {{ company.company_name }}</p>
            <a href="https://thoriumdesign.com"><p>Designed and developed by Thorium Design, LLC</p></a>
        </b-container>
    </b-row>
</template>

<script>
import homeJSON from '~/content/data/home.json'
import companyJSON from '~/content/data/company.json'

export default {
  data () {
    return {
      home: homeJSON,
      company: companyJSON,
      phone: companyJSON.phone
    }
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
    
    },
    year() {
        return new Date().getFullYear()
    }
  }
}
</script>

<style lang="scss" scoped>
$primary-color: var(--primary-color);
$primary-hover: var(--primary-hover);

.th {
  &__footer {
    background: $primary-color;
    color: white;
    padding-top: 80px;
    padding-bottom: 100px;
    .container {
        max-width: 480px;
    }
    p {
        margin-bottom: 0;
    }
    a {
        color: white;
        text-decoration: underline;
        p {
            margin-top: 24px;
        }
    }
  }
}
</style>

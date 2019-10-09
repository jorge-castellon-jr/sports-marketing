<template>
<b-row class="th__header" align-v="center" :style="cssProps">
    <b-col class="th__logo">
        <b-img :src="`${company.logo}`"></b-img>
    </b-col>
    <b-col class="th__phone">
        <a :href="`tel:${phone}`">
            <phoneSVG />
        </a>
    </b-col>
</b-row>
</template>

<script>
import homeJSON from '~/content/data/home.json'
import companyJSON from '~/content/data/company.json'
import phoneSVG from '~/components/PhoneSVG.vue'

export default {
    data () {
        return {
            home: homeJSON,
            company: companyJSON,
            phone: companyJSON.phone
        }
    },
    components: {
        phoneSVG
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
                return JSON.stringify(formated)
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

.th {
    &__header {
        padding: 10px 16px;
        @media only screen and (min-width: 576px) {
            padding: 10px 24px;
        }
    }
    &__logo {
        img {
            max-width: 150px;
            max-height: 52px;
        }
    }
    &__phone {
        a {
            display: flex;
            justify-content: flex-end;
            align-items: center;
            transition: color .3s;
            &:hover, &:hover:before {
                text-decoration: none;
                color: $primary-hover;
            }
            &:hover svg {
                fill: $primary-hover;
            }
            &:before {
                content: 'CALL';
                font-size: 20px;
                font-family: proxima-nova, sans-serif;
                padding-right: 6px;
                text-decoration: none;
                color: $primary-color;
            }
            @media only screen and (min-width: 576px) {
                &:before {
                    content: var(--phone);
                    font-size: 20px;
                }
            }
        }
        svg {
            transition: fill .3s;
            max-width: 36px;
            max-height: 36px;
            fill: $primary-color;
            
        }
    }
}
</style>
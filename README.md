# vuetify-swipeout
This project is a swipe out example built with [Vue], [Vuetify] and [Swiper]. 

[Vue.js]: https://vuejs.org
[Swiper]: http://idangero.us/swiper/
[Vuetify]: https://vuetifyjs.com

<p align="center">
  <a href="https://vuetifyswipeout.davidgaroro.es" target="_blank" rel="noopener">
    <img src="https://vuetifyswipeout.davidgaroro.es/github/app.gif"><br/>
    Live Demo
  </a>
</p>

## Features
- Vue CLI 3 + Webpack + vue-loader for single file Vue components
  - Hot-reload in development
  - Lint-on-save with [ESLint (Standard)](https://github.com/standard/eslint-config-standard)
  - Stylus CSS preprocessor
- Vuetify a-la-carte (reduce project's size  in production)
- Progressive Web App
  - App manifest
  - Service worker
  - Workbox options - [Cache Google Fonts]
  - 100/100 Lighthouse score

[Cache Google Fonts]: https://developers.google.com/web/tools/workbox/guides/common-recipes#google_fonts

## Built With
### Dependencies
| Name| Description | |
|--|--|:--:| 
|[swiper]|️Most Modern Mobile Touch Slider|👆
|[vue]|Progressive JavaScript Framework|🖖
|[vue-cli-3]|️Standard Tooling for Vue.js Development|🛠️
|[vuetify]|️Material Component Framework for Vue.js|📚

[swiper]: http://idangero.us/swiper
[vue]: https://vuejs.org
[vue-cli-3]: https://cli.vuejs.org
[vuetify]: https://vuetifyjs.com

### Development Dependencies
| Name| Description | |
|--|--|:--:| 
|[stylus-loader]|CSS preprocessor for webpack|🎨
|[vue/cli-plugin-babel]|Compiler for next generation JavaScript|🐠
|[vue/cli-plugin-eslint]|Pluggable JavaScript linter|✍️
|[vue/cli-plugin-pwa]|JavaScript Library for adding support to PWA|📱

[stylus-loader]: https://github.com/shama/stylus-loader
[vue/cli-plugin-babel]: https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel
[vue/cli-plugin-eslint]: https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint
[vue/cli-plugin-pwa]: https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-pwa

## How To Use Swiper with Vuetify

> For information on how to use Swiper, visit the [official documentation]

[official documentation]: http://idangero.us/swiper/get-started/

### Install Swiper
```
npm install swiper --save
```

### Add v-list component
``` vue
<!-- App.vue -->
<template>
  ...
  <v-list>
    <template v-for="(item, index) in items">
      <custom-component
        :id="`item-${item}`"
        @transitionEnd="customFunction"
        ...
      />
      <v-divider...></v-divider>
    </template>
  </v-list>
  ...
</template>

<script>
import CustomComponent from '@/components/CustomComponent.vue'
export  default {
  components: {
    'custom-component': CustomComponent
  },
  methods: {
    transitionEnd () {
      // Callback from SwipeoutItem after transition
      ...
    }
  }
}
</script>
```

### Import and configure Swiper in the custom component
``` vue
<!-- CustomComponent.vue -->
<template>
  <div :id="id" class="swiper-container">
    <div class="swiper-wrapper">
      <v-list-tile class="swiper-slide error"></v-list-tile>
      <v-list-tile class="swiper-slide">
        <!-- custom content here -->
      </v-list-tile>
    </div>
  </div>
</template>

<script>
import 'swiper/dist/css/swiper.min.css'
import { Swiper } from 'swiper/dist/js/swiper.esm.js'

export default {
  props: ['id'],
  mounted () {
    const self = this
    const el = '#' + this.id

    // Initialize Swiper
    const swiper = new Swiper(el, {
      initialSlide: 1,
      resistanceRatio: 0,
      speed: 150
    })

    // Event will be fired after transition
    swiper.on('transitionEnd', function () {
      if (this.activeIndex === 0) {
        self.$emit('transitionEnd')
        // Destroy slider instance and detach all events listeners
        this.destroy()
      }
    })
  }
}
</script>
```

## Project Installation & Setup
### Clone repository
```
git clone https://github.com/davidgaroro/vuetify-swipeout.git
cd vuetify-swipeout
```

### Install dependencies
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```
## Donation
[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/donate?hosted_button_id=T7CVYXY994KHJ)
## License
[MIT](./LICENSE) &copy; davidgaroro

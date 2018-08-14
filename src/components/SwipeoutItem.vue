<template>
  <div :id="id" class="swiper-container">
    <div class="swiper-wrapper">

      <!-- swipe right template -->
      <template v-if="direction == 'right'">
        <v-list-tile class="swiper-slide error"></v-list-tile>
        <v-list-tile class="swiper-slide">
          <v-list-tile-content>
            <v-list-tile-title>
              {{ `${item} - Swipe me to ${direction}` }}
            </v-list-tile-title>
          </v-list-tile-content>
          <v-list-tile-action>
            <v-icon color="primary">arrow_forward</v-icon>
          </v-list-tile-action>
        </v-list-tile>
      </template>

      <!-- swipe left template -->
      <template v-if="direction == 'left'">
        <v-list-tile class="swiper-slide">
          <v-list-tile-action>
            <v-icon color="primary">arrow_back</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title class="text-xs-right">
              {{ `Swipe me to ${direction} - ${item}` }}
            </v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile class="swiper-slide error"></v-list-tile>
      </template>

    </div>
  </div>
</template>

<script>
import 'swiper/dist/css/swiper.min.css'
import { Swiper } from 'swiper/dist/js/swiper.esm.js'

export default {
  props: {
    id: [String],
    item: [Number],
    direction: {
      validator: value => {
        return ['right', 'left'].indexOf(value) !== -1
      }
    }
  },
  mounted () {
    const self = this
    const el = '#' + this.id
    const direction = this.direction

    // Initialize Swiper
    const swiper = new Swiper(el, {
      initialSlide: this.direction === 'left' ? 0 : 1,
      resistanceRatio: 0,
      speed: 150
    })

    // Event will be fired after transition
    swiper.on('transitionEnd', function () {
      const activeIndex = this.activeIndex
      if ((direction === 'right' && activeIndex === 0) || (direction === 'left' && activeIndex === 1)) {
        self.$emit('transitionEnd')
        // Destroy slider instance and detach all events listeners
        this.destroy()
      }
    })
  }
}
</script>

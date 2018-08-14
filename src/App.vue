<template>
  <v-app id="app">
    <v-content>
      <v-container id="container">
        <v-layout row wrap>
          <v-flex text-xs-center>
            <!-- header -->
            <h1 class="primary--text display-3 font-weight-medium my-3">Swipeout</h1>

            <!-- swipe right section -->
            <v-card class="mb-4" v-if="itemsRight.length">
              <v-list class="pa-0">
                <template v-for="(item, index) in itemsRight">
                  <SwipeoutItem
                    :item="item"
                    direction="right"
                    :id="`item-right-${item}`"
                    :key="`item-right-${item}`"
                    @transitionEnd="transitionEnd(itemsRight, index)"
                  />
                  <v-divider
                    v-if="index + 1 < itemsRight.length"
                    :key="`divider-right-${item}`"
                  />
                </template>
              </v-list>
            </v-card>

            <!-- swipe left section -->
            <v-card class="mb-4" v-if="itemsLeft.length">
              <v-list class="pa-0">
                <template v-for="(item, index) in itemsLeft">
                  <SwipeoutItem
                    :item="item"
                    direction="left"
                    :id="`item-left-${item}`"
                    :key="`item-left-${item}`"
                    @transitionEnd="transitionEnd(itemsLeft, index)"
                  />
                  <v-divider
                    v-if="index + 1 < itemsLeft.length"
                    :key="`divider-left-${item}`"
                  />
                </template>
              </v-list>
            </v-card>

            <h3 v-if="!itemsRight.length && !itemsLeft.length" class="headline my-4 grey--text">There is no data!</h3>
            <v-btn color="primary" depressed block round @click="resetData">Reset data</v-btn>

            <!-- footer -->
            <footer class="caption">
              <p>Written by <a href="https://github.com/davidgaroro" target="_blank" rel="noopener">davidgaroro</a></p>
              <p><a href="https://github.com/davidgaroro/vuetify-swipeout" target="_blank" rel="noopener">View on GitHub</a></p>
            </footer>

          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import SwipeoutItem from '@/components/SwipeoutItem.vue'

const itemsRight = [ 1, 2, 3, 4 ]
const itemsLeft = [ 5, 6, 7, 8 ]

export default {
  name: 'app',
  components: {
    SwipeoutItem
  },
  data () {
    return {
      itemsRight: itemsRight.slice(),
      itemsLeft: itemsLeft.slice()
    }
  },
  methods: {
    resetData () {
      this.itemsRight = itemsRight.slice()
      this.itemsLeft = itemsLeft.slice()
    }
  }
}
</script>

<style lang="stylus" scope>
#app
  background: #f5f5f5
  h1
    opacity: 0.3
  #container
    max-width: 360px
    padding: 8px
  footer
    margin: 65px auto 0
    color: #bfbfbf
    text-shadow: 0 1px 0 rgba(255, 255, 255, 0.5)
    p
      line-height: 1
    a
      color: inherit
      text-decoration: none
      &:hover
        text-decoration: underline
</style>

<template>
  <div :id="id">

    <!-- swipe right template -->
    <template v-if="direction == 'right'">
      <v-list-tile>
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
      <v-list-tile>
        <v-list-tile-action>
          <v-icon color="primary">arrow_back</v-icon>
        </v-list-tile-action>
        <v-list-tile-content>
          <v-list-tile-title class="text-xs-right">
            {{ `Swipe me to ${direction} - ${item}` }}
          </v-list-tile-title>
        </v-list-tile-content>
      </v-list-tile>
    </template>

  </div>
</template>

<script>
export default {
  props: {
    id: [String],
    item: [Number],
    direction: {
      validator: value => {
        return ['right', 'left'].indexOf(value) !== -1
      }
    }
  }
}
</script>

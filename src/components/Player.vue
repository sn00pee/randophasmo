<script lang="ts">
import { defineComponent } from 'vue'

export type Item =
  | 'flashlight'
  | 'dots'
  | 'camera'
  | 'lighter'
  | 'smudge'
  | 'candle'
  | 'cam'
  | 'spirit'
  | 'strong_flashlight'
  | 'uv_light'
  | 'tripod'
  | 'pills'
  | 'thermometer'
  | 'salt'
  | 'mic'
  | 'parabolic_mic'
  | 'crucifix'
  | 'motion'
  | 'emf'
  | 'book'

export interface Items {
  pairs?: Array<Item>
  id: Item
  title: string
  capacity: number
}

export interface Person {
  name: string
  id: number
  items?: Array<Items>
}

export default defineComponent({
  // type inference enabled
  props: {
    name: String,
    playerId: Number,
    items: Array<Items>,
  },
  methods: {
    removePlayer() {
      this.$emit('removePlayer', this.playerId)
    },
  },
})
</script>

<template>
  <div>
    <h1 :class="$style.name">{{ name }}</h1>
    <span :class="$style.remove" @click="removePlayer">remove</span>
    <ul :class="$style.items">
      <li :class="$style.item" v-for="item in items">{{ item.title }}</li>
    </ul>
  </div>
</template>

<style lang="scss" module>
.name {
  margin-bottom: 5px;
}

.remove {
  color: red;
  display: block;
  cursor: pointer;
  font-size: 10px;
  margin-top: 5px;
}

.items {
  box-sizing: border-box;
  list-style-type: disc;
  margin: 20px 0;
  padding: 0;
  min-height: 102px;
}

.item {
  text-align: end;
  padding: 5px;
}
</style>

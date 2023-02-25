<script lang="ts">
import { defineComponent } from 'vue'
import Player, { Person, Items, Item } from './components/Player.vue'

const itemList = [
  {
    pairs: [],
    id: 'flashlight',
    title: 'Flashlight',
    capacity: 4,
  },
  {
    pairs: [],
    id: 'dots',
    title: 'D.O.T.S.',
    capacity: 2,
  },
  {
    pairs: [],
    id: 'camera',
    title: 'Photo Camera',
    capacity: 4,
  },
  {
    pairs: ['candle', 'smudge'],
    id: 'lighter',
    title: 'Lighter',
    capacity: 4,
  },
  {
    pairs: ['lighter'],
    id: 'smudge',
    title: 'Smudge Stick',
    capacity: 4,
  },
  {
    pairs: ['lighter'],
    id: 'candle',
    title: 'Candle',
    capacity: 4,
  },
  {
    pairs: [],
    id: 'cam',
    title: 'Video Camera',
    capacity: 4,
  },
  {
    pairs: [],
    id: 'spirit',
    title: 'Spirit Box',
    capacity: 2,
  },
  {
    pairs: [],
    id: 'strong_flashlight',
    title: 'Strong Flashlight',
    capacity: 4,
  },
  {
    pairs: [],
    id: 'uv_light',
    title: 'UV flashlight',
    capacity: 3,
  },
  {
    pairs: ['cam'],
    id: 'tripod',
    title: 'Tripod',
    capacity: 4,
  },
  {
    pairs: [],
    id: 'pills',
    title: 'Sanity Pills',
    capacity: 4,
  },
  {
    pairs: [],
    id: 'thermometer',
    title: 'Thermometer',
    capacity: 2,
  },
  {
    pairs: [],
    id: 'salt',
    title: 'Salt',
    capacity: 3,
  },
  {
    pairs: [],
    id: 'mic',
    title: 'Floor Microphone',
    capacity: 4,
  },
  {
    pairs: [],
    id: 'parabolic_mic',
    title: 'Parabolic Microphone',
    capacity: 2,
  },
  {
    pairs: [],
    id: 'crucifix',
    title: 'Crucifix',
    capacity: 2,
  },
  {
    pairs: [],
    id: 'motion',
    title: 'Motion Sensor',
    capacity: 4,
  },
  {
    pairs: [],
    id: 'emf',
    title: 'EMF Reader',
    capacity: 2,
  },
  {
    pairs: [],
    id: 'book',
    title: 'Ghost Writing Book',
    capacity: 2,
  },
] as Array<Items>

export default defineComponent({
  components: {
    Player,
  },
  data: () => ({
    name: '',
    players: [] as Array<Person>,
    max: 4,
    itemList,
  }),
  computed: {
    maxPlayers(): boolean {
      return this.players.length === this.max
    },
    playerNameUnique(): boolean {
      return this.name !== '' && !this.players.some((player) => player.name === this.name)
    },
  },
  methods: {
    addPlayer() {
      this.players.push({
        name: this.name,
        id: this.players.length,
        items: [],
      })
    },
    randomize(id: number) {
      this.players[id].items = [...this.itemList].sort(() => 0.5 - Math.random()).slice(0, 3)
    },
    handleRemove(id: number) {
      this.players.splice(id, 1)
    },
  },
})
</script>

<template>
  <div :class="$style.box" v-if="!maxPlayers">
    <input type="text" :class="$style.name" v-model="name" />
    <button :class="$style.button" @click="addPlayer" :disabled="!playerNameUnique">add</button>
  </div>
  <ul :class="$style.list">
    <li :class="$style.item" v-for="(player, index) in players">
      <Player :name="player.name" :player-id="index" :items="player.items" @removePlayer="handleRemove" />
      <button :class="$style.random" @click.prevent="randomize(index)">Randomize items</button>
    </li>
  </ul>
</template>

<style lang="scss" module>
.name {
  margin-right: 3px;
  background: transparent;
  border: none;
  border-bottom: 3px solid #1a1a1a;
  font-size: 14px;
  height: 100%;
  padding: 13px 52px 11px 13px;
  width: 100%;

  &:focus,
  &:hover {
    outline: none;
  }
}

.box {
  display: flex;
  align-items: center;
  justify-content: center;
}
.button {
  margin-left: 5px;
}

.random {
  margin-top: 10px;
  padding: 5px 10px;
}
.list {
  display: grid;
  gap: 30px;
  grid-template-columns: repeat(2, auto);
  padding: 0;
  list-style: none;
  margin: 10px 0 10px 0;
}

.item {
  padding: 5px;
}
</style>

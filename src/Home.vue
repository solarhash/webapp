<template>
  <div>
    <div class="header">solarhash</div>
    <div class="container">
      <div>
        <input type="text" v-model="hash" v-on:change="hashChanged" />
        <button v-on:click="generateHash">Generate Hash</button>
      </div>
      <div style="font-family: monospace">
        <p style="white-space:pre-wrap">{{ hashart }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import Component from 'vue-class-component'
import solarhash from 'solarhash'

@Component({
  name: 'Home',
  components: {},
  metaInfo: {
    title: 'Solarhash',
  },
})
export default class Home extends Vue {
  hash = ''
  hashart = ''

  hashChanged() {
    console.log('updated!', this.hash)
    this.updateArt()
  }

  generateHash() {
    let hash = '0x'
    for (let x = 0; x < 40; x++) {
      hash += (Math.floor(Math.random() * 16)).toString(16)
    }
    this.hash = hash
    this.updateArt()
  }

  updateArt() {
    this.hashart = solarhash(this.hash)
  }

  async serverPrefetch() {
    // probably calculate a hash here
  }

  async mounted() {
  }
}
</script>

<style scoped>
.header {
  font-size: 30px;
}
.container {
  display: flex;
}
</style>

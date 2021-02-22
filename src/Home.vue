<template>
  <div>
    <div class="header">solarhash</div>
    <div class="container">
      <div>
        <input style="width: 500px" type="text" v-model="hash" @input="hashChanged" />
        <div>
          <button v-on:click="generateShortHash">Generate Hash</button>
          <button v-on:click="generateLongHash">Generate Long Hash</button>
        </div>
      </div>
      <div style="font-family: monospace">
        <p style="white-space:pre-wrap; ; font-size: 20px">{{ hashart }}</p>
        <p>{{ info }}<span v-if="showWarning" style="color: red"> !! Art is not unique</span></p>
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
  info = ''
  showWarning = false

  hashChanged() {
    this.updateArt()
  }

  generateShortHash() {
    this.hash = this.generateHash(20)
    this.updateArt()
  }

  generateLongHash() {
    this.hash = this.generateHash(32)
    this.updateArt()
  }

  generateHash(bytes) {
    let hash = '0x'
    for (let x = 0; x < bytes*2; x++) {
      hash += (Math.floor(Math.random() * 16)).toString(16)
    }
    return hash
  }

  updateArt() {
    const { art, bitsConsumed, bits } = solarhash(this.hash)
    this.hashart = art
    this.info = `Used ${bitsConsumed} of ${bits} bits`
    this.showWarning = bitsConsumed < bits
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

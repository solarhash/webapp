<template>
  <div>
    Hello World
  </div>
</template>

<script>
import Vue from 'vue'
import Component from 'vue-class-component'

@Component({
  name: 'Home',
  components: {},
  metaInfo: {
    title: 'Solarhash',
  },
})
export default class Home extends Vue {
  async serverPrefetch() {
    // probably calculate a hash here
  }

  async mounted() {
  }
}
</script>

<style scoped>
</style>

<template>
  <div id="app">
    <SlotMachine
      :isRandom="isRandom"
      :slot1="slot1"
      :slot2="slot2"
      :slot3="slot3"
    />
    <DebugPanel
    @isRandom="debugPanelSetIsRandom"
    @slot1="slot1Selected"
    @slot2="slot2Selected"
    @slot3="slot3Selected"/>
  </div>
</template>

<script>
import SlotMachine from './components/SlotMachine.vue'
import DebugPanel from './components/DebugPanel.vue'
export default {
  name: 'app',
  components: {
    SlotMachine,
    DebugPanel
  },
  data () {
    return {
      isRandom: true,
      slot1: null,
      slot2: null,
      slot3: null
    }
  },
  methods: {
    debugPanelSetIsRandom(value) {
        this.isRandom = value
    },
    slot1Selected(selection) {
      this.slot1 = selection
    },
    slot2Selected(selection) {
      this.slot2 = selection
    },
    slot3Selected(selection) {
      this.slot3= selection
    }

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

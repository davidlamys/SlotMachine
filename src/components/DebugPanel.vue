<template>
  <div class="debug-panel">
    <input type="radio" id="one" value=false @input="setIsRandom" v-model="random">
    <label for="fixed">Fixed</label>
    <input type="radio" id="two" value=true @input="setIsRandom" v-model="random">
    <label for="random">Random</label>
    <br>
    <span>Picked: {{ random }}</span>
    <br>
    <br>
    <div class="fixedChoices">
      <div id="choice1">
        <input type="radio" id="choice1_0" value=0 @input="$emit('slot1', $event.target.value)" v-model="choice1">
        <label>3xBAR</label>
        <input type="radio" id="choice1_1" value=1 @input="$emit('slot1', $event.target.value)" v-model="choice1">
        <label>BAR</label>
        <input type="radio" id="choice1_2" value=2 @input="$emit('slot1', $event.target.value)" v-model="choice1">
        <label>2xBAR</label>
        <input type="radio" id="choice1_3" value=3 @input="$emit('slot1', $event.target.value)" v-model="choice1">
        <label>7</label>
        <input type="radio" id="choice1_4" value=4 @input="$emit('slot1', $event.target.value)" v-model="choice1">
        <label>CHERRY</label>
        <br>
      </div>
      <div id="choice2">
        <input type="radio" id="choice2_0" value=0 @input="$emit('slot2', $event.target.value)" v-model="choice2">
        <label>3xBAR</label>
        <input type="radio" id="choice2_1" value=1 @input="$emit('slot2', $event.target.value)" v-model="choice2">
        <label>BAR</label>
        <input type="radio" id="choice2_2" value=2 @input="$emit('slot2', $event.target.value)" v-model="choice2">
        <label>2xBAR</label>
        <input type="radio" id="choice2_3" value=3 @input="$emit('slot2', $event.target.value)" v-model="choice2">
        <label>7</label>
        <input type="radio" id="choice2_4" value=4 @input="$emit('slot2', $event.target.value)" v-model="choice2">
        <label>CHERRY</label>
        <br>
      </div>
      <div id="choice3">
        <input type="radio" id="choice3_0" value=0 @input="$emit('slot3', $event.target.value)" v-model="choice3">
        <label>3xBAR</label>
        <input type="radio" id="choice3_1" value=1 @input="$emit('slot3', $event.target.value)" v-model="choice3">
        <label>BAR</label>
        <input type="radio" id="choice3_2" value=2 @input="$emit('slot3', $event.target.value)" v-model="choice3">
        <label>2xBAR</label>
        <input type="radio" id="choice3_3" value=3 @input="$emit('slot3', $event.target.value)" v-model="choice3">
        <label>7</label>
        <input type="radio" id="choice3_4" value=4 @input="$emit('slot3', $event.target.value)" v-model="choice3">
        <label>CHERRY</label>
        <br>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DebugPanel",
  methods: {
    setIsRandom() {
      console.log(this.random)
      this.$emit('isRandom', (this.random == "true"))
    }
  },
  data() {
    return {
      random: true,
      choice1: "3xBAR",
      pos1: "top",
      choice2: "3xBAR",
      pos2: "top",
      choice3: "3xBAR",
      pos3: "top"
    }
  }
}
</script>

/* eslint-disable */
<template>
  <div class='slot-machine'>
    <button @click='start'>
      start
    </button>
    <div class='slot' v-for='slot in slots' ref='slots'>
      <div class='slot__window'>
        <div class='slot__wrap'>
          <div class='slot__item' v-for='opt in slot.items'>{{ opt }}</div>
          <div class='slot__item slot__item--copy' >{{ slot.items[0] }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const next = window.requestAnimationFrame ||
window.webkitRequestAnimationFrame ||
window.mozRequestAnimationFrame ||
window.msRequestAnimationFrame ||
window.oRequestAnimationFrame ||
function(cb) { window.setTimeout(cb, 1000/60) }

export default {
  name: 'SlotMachine',
  props: {
    "isRandom": Boolean,
    "slot1": String,
    "slot2": String,
    "slot3": String
  },
  data() {
    return {
      slots: [{
        items: [
          "3xBAR",
          "BAR",
          "2xBAR",
          "7",
          "CHERRY"
        ]
      }, {
        items: [
          "3xBAR",
          "BAR",
          "2xBAR",
          "7",
          "CHERRY"
        ]
      }, {
        items: [
          "3xBAR",
          "BAR",
          "2xBAR",
          "7",
          "CHERRY"
        ]
      }],
      opts: null,
      startedAt: null,
    }
  },

  methods: {
    start: function() {

      if (this.opts) {
        return
      }

      this.opts = this.slots.map( (data, i) => {

        const slot = this.$refs.slots[i]
        const debugChoice = i == 0 ? this.slot1 : (i == 1 ? this.slot2 : this.slot3)
        const randomChoice = Math.floor( Math.random() * data.items.length )
        const choice = this.isRandom ? randomChoice : debugChoice
        const isMiddle = Math.random() >= 0.5
        console.log("choice", choice, data.items[choice], isMiddle)
        const finalPos = choice * 180 - (isMiddle ? 90 : 0)

        const opts = {
          el: slot.querySelector('.slot__wrap'),
          finalPos: finalPos  ,
          startOffset: 2000 + Math.random() * 500 + i * 500,
          height: data.items.length * 180,
          duration: 3000 + i * 700, // milliseconds
          isFinished: false,
        }

        return opts

      })

      next( this.animate )

    },

    animate: function(timestamp) {

      if (this.startedAt == null) {
        this.startedAt = timestamp
      }

      const timeDiff = timestamp - this.startedAt

      this.opts.forEach( opt => {

        if (opt.isFinished) {
          return
        }

        const timeRemaining = Math.max(opt.duration - timeDiff, 0)
        const power = 3
        const offset = ( Math.pow(timeRemaining, power) / Math.pow(opt.duration, power) ) * opt.startOffset

        // negative, such that slots move from top to bottom
        const pos = -1 * Math.floor((offset + opt.finalPos) % opt.height)

        opt.el.style.transform = "translateY(" + pos + "px)"

        if ( timeDiff > opt.duration ) {
          console.log('finished', opt, pos, opt.finalPost)
          opt.isFinished = true
        }

      })

      if (this.opts.every( o => o.isFinished )) {
        this.opts = null
        this.startedAt = null
        console.log('finished')
      } else {
        next( this.animate )
      }

    }
  }
}
</script>

<style>
.slot {
  float: left;
  margin: 0.4em;
}

.slot__window {
  background-color: green;
  width: 200px;
  height: 380px;
  overflow: hidden;
}

.slot__wrap {

}

.slot__item {
  margin-top: 20px;
  height: 160px;
  width: 180px;
  padding: 0 10px;

  text-align: center;
  background-color: blue;
  color: white;

  line-height: 160px;
}

.slot__item--copy {
}
</style>

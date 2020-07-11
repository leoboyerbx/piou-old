<template>
  <div id="grapes">
    <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" :viewBox="viewBox" style="overflow:visible;enable-background:new 0 0 687 840;" xml:space="preserve">
    <circle v-for="grape in grapes" :class="grape.colorClass" :key="grape.key" :cx="grape.cx" :cy="grape.cy" :r="grapeRad" />
</svg>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

const pickRandom = (array: Array<any>): any => (array[Math.floor(Math.random() * array.length)])

export default Vue.extend({
  name: 'Grapes',
  props: {
    lines: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      grapeRad: 20,
      margin: 1
      // linesNum: 5
    }
  },
  computed: {
    linesNum (): number {
      return parseInt(this.lines)
    },
    grapeDiam (): number {
      return this.grapeRad * 2
    },
    nMax (): number {
      return (this.linesNum - 1)
    },
    viewBox (): string {
      const xMax = (this.nMax * this.grapeDiam) + ((this.nMax - 1) * this.margin)
      const yMax = this.linesNum * this.grapeDiam
      return `0 0 ${xMax} ${yMax}`
    },
    grapes (): Array<Record<string, any>> {
      const grapes = []
      for (let i = 1; i <= this.linesNum; i++) {
        const n = (i === this.linesNum) ? this.linesNum - 2 : i
        const lineY = this.grapeRad + (this.linesNum - i) * this.grapeDiam

        const offset = ((this.nMax - n) * this.grapeRad + (this.nMax - n - 1) * this.margin / 2)
        // if (isOdd(n)) offset += this.grapeRad + (this.margin/2)

        for (let g = 0; g < n; g++) {
          grapes.push({
            key: `${i}${g}`,
            cx: this.grapeRad + g * (this.grapeDiam + this.margin) + offset,
            cy: lineY,
            colorClass: pickRandom(['color1', 'color2', 'color0'])
          })
        }
      }
      return grapes
    }
  }

})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.color0{fill:#5D73D8;}
.color1{fill:#778DE0;}
.color2{fill:#3560BF;}

#grapes {
  width: 50%;

  svg {
    width: 100%;
  }
}
</style>

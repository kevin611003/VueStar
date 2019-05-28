<template>
  <div class="VueStar">
    <div class="VueStar__ground">
      <div class="VueStar__icon" @click="toggle" :class="AnimateClass" :style="{color:ColorValue}">
        <slot name="icon"></slot>
      </div>
      <div class="VueStar__decoration" :class="{'VueStar__decoration--active': isActive}"></div>
    </div>
  </div>
</template>

<script>
import { isColors } from '../uitls/colorRE.js'
export default {
  name: 'VueStar',
  props: {
    animate: {
      type: String,
      default: ''
    },
    color: {
      type: String,
      default: ''
    },
    active: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      isActive: this.active
    }
  },
  computed: {
    AnimateClass () {
      return this.isActive ? this.animate : ''
    },
    ColorValue () {
      return this.isActive ? this.color : ''
    }
  },
  mounted () {
    if (this.color) {
      if (!isColors(this.color)) {
        console.error('this color must be hexcolor or rgbcolor  ---VueStar')
      }
    }
  },
  methods: {
    toggle () {
      if (!this.disabled) {
        this.isActive = !this.isActive
        this.$emit('toggle', this.isActive)
      }
    }
  }
}
</script>

<style lang="less">
 @import '../style/main.less';
</style>

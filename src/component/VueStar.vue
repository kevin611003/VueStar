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
      isActive: false,
      AnimateClass: '',
      ColorValue: ''
    }
  },
  mounted () {
    if (this.color) {
      if (!isColors(this.color)) {
        console.error('this color must be hexcolor or rgbcolor  ---VueStar')
      }
    }

    this.isActive = this.active
    if (this.isActive) {
      this.ColorValue = this.color
    }
  },
  methods: {
    toggle () {
      if (!this.disabled) {
        this.isActive = !this.isActive

        if (this.isActive) {
          this.AnimateClass = this.animate
          this.ColorValue = this.color
        } else {
          this.AnimateClass = ''
          this.ColorValue = ''
        }

        this.$emit('toggle', this.isActive)
      }
    }
  }
}
</script>

<style lang="less">
 @import '../style/main.less';
</style>

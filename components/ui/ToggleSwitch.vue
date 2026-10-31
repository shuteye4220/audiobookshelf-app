<template>
  <div>
    <button type="button" role="switch" :aria-checked="toggleValue ? 'true' : 'false'" :aria-label="label || null" :aria-disabled="disabled ? 'true' : null" class="border rounded-full border-gray-400 flex items-center cursor-pointer w-10 justify-start p-0" :class="className" @click.stop="clickToggle">
      <span class="rounded-full border w-5 h-5 border-gray-100 shadow transform transition-transform duration-100" :class="switchClassName" aria-hidden="true"></span>
    </button>
  </div>
</template>

<script>
export default {
  props: {
    value: Boolean,
    // Accessible name read by screen readers, normally the setting's visible label text
    label: String,
    onColor: {
      type: String,
      default: 'success'
    },
    offColor: {
      type: String,
      default: 'primary'
    },
    disabled: Boolean
  },
  computed: {
    toggleValue: {
      get() {
        return this.value
      },
      set(val) {
        this.$emit('input', val)
      }
    },
    className() {
      if (this.disabled) return this.toggleValue ? `bg-${this.onColor} cursor-not-allowed` : `bg-${this.offColor} cursor-not-allowed`
      return this.toggleValue ? `bg-${this.onColor}` : `bg-${this.offColor}`
    },
    switchClassName() {
      var bgColor = this.disabled ? 'bg-gray-300' : 'bg-white'
      return this.toggleValue ? 'translate-x-5 ' + bgColor : bgColor
    }
  },
  methods: {
    clickToggle() {
      if (this.disabled) return
      this.toggleValue = !this.toggleValue
    }
  }
}
</script>

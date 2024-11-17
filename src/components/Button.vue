<template>
  <button 
    :class="buttonClasses" 
    @click="$emit('click')"
  >
    <span v-if="icon" class="icon" :class="iconClasses">{{ icon }}</span>
    {{ label }}
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    label: {
      type: String,
      required: true
    },
    color: {
      type: String,
      default: 'blue'
    },
    size: {
      type: String,
      default: 'medium'
    },
    icon: {
      type: String,
      default: ''
    }
  },
  computed: {
    buttonClasses() {
      return [
        'py-2', 'px-4', 'font-semibold', 'rounded-lg', 'inline-flex', 'items-center', 'focus:outline-none',
        this.getColorClass(),
        this.getSizeClass()
      ];
    },
    iconClasses() {
      return [
        'mr-2'
      ];
    }
  },
  methods: {
    getColorClass() {
      switch (this.color) {
        case 'red':
          return 'bg-red-500 hover:bg-red-700 text-white';
        case 'green':
          return 'bg-green-500 hover:bg-green-700 text-white';
        case 'blue':
        default:
          return 'bg-blue-500 hover:bg-blue-700 text-white';
      }
    },
    getSizeClass() {
      switch (this.size) {
        case 'small':
          return 'text-sm';
        case 'large':
          return 'text-lg';
        case 'medium':
        default:
          return 'text-base';
      }
    }
  }
}
</script>

<style scoped>
.icon {
  display: inline-flex;
  align-items: center;
}
</style>

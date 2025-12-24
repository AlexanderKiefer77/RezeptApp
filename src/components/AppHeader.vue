<template>
  <header>
    <input
      type="text"
      placeholder="Suche..."
      v-model="search"
    />
  </header>
</template>

<script>
export default {
  name: 'AppHeader',

  props: {
    modelValue: {
      type: String,
      default: ''
    }
  },

  computed: {
    search: {
      get() {
        return this.modelValue
      },
      set(value) {
        this.$emit('update:modelValue', value)
      }
    }
  }
}
</script>


<style scoped>
header {
    background-color: #F4BC39;
    height: 80px;
    padding: 16px;
    display: flex;
    align-items: flex-end;
}

input {
    border: 0;
    border-radius: 8px;
    width: 100%;
    height: 30px;
}
</style>
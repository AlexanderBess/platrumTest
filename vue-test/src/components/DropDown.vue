<template>
  <select
    v-model="searchQuery"
    :disabled="bosses.length === 0"
    class="dropdown">
    <option
      v-for="(option, key) in bosses"
      :key="key">
      {{ option }}
    </option>
  </select>
</template>

<script>

export default {
  name: 'DropDown',
  props: {
    value: {
      required: true
    },
    bosses: {
      required: true
    }
  },
  computed: {
    searchQuery: {
      get () {
        return this.value
      },
      set (value) {
        this.$emit('select', value)
      }
    }
  }
}
</script>

<style scoped>
.dropdown {
  max-width: 177px;
  height: 21px;
  width: 100%;
}
</style>

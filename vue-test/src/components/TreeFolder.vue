<template>
  <ul>
    <li
      v-for="(user, key) in padawans"
      :key="key">
      {{ isName ? user.name : user.phone }}
      <tree-folder
        v-if="user.padawans"
        :padawans="user.padawans"
        :isName="isName"/>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'TreeFolder',
  props: {
    padawans: {
      required: true
    },
    isName: {
      required: false
    }
  }
}
</script>

<style scoped>

</style>

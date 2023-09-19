<template>
  <div class="table">
    <table class="table__content">
      <template v-if="users.length === 0">
        <span>Добавьте нового пользователя</span>
      </template>
      <template v-else>
        <caption class="table__title">Список пользователей</caption>
        <tr>
          <td class="table__cell">Имя</td>
          <td class="table__cell">Телефон</td>
        </tr>
        <tr
          v-for="(item, key) in users"
          :key="key">
          <td class="table__cell">
            <ul>
              <li>
                {{ item.name }}
                <tree-folder :padawans="item.padawans" :is-name="true"/>
              </li>
            </ul>
          </td>
          <td class="table__cell">
            <ul>
              <li>
                {{ item.phone }}
                <tree-folder :padawans="item.padawans" :is-name="false"/>
              </li>
            </ul>
          </td>
        </tr>
      </template>
    </table>
  </div>
</template>

<script>
import TreeFolder from './TreeFolder'

export default {
  name: 'Table',
  components: { TreeFolder },
  props: {
    users: {
      required: true
    }
  }
}
</script>

<style scoped>
.table {
  margin: 15px;
}
.table__content {
  width: 100%;
  border-spacing: 0;
}
.table__title {
  padding: 5px 10px;
  font-size: 18px;
}
.table__cell {
  padding: 3px 5px;
  border: 1px solid gray;
}
</style>

<template>
  <div class="page">
    <img
      :class="newUserAdded ? 'surprise surprise_active': 'surprise'"
      src="https://media.graphassets.com/LVxBf0jTeyzy7HZrfavn"
      alt="Giphy Brand Ranking OMR"
      data-v-56e3df82="">
    <div id="app">
      <button
        class="btn"
        @click="isShowModal = true">
        Добавить
      </button>
      <base-table :users="usersData"/>
    </div>
    <base-modal
      v-show="isShowModal"
      :bosses="bossesData"
      @close="isCloseModal"
      @save="addedNewUser"/>
  </div>
</template>

<script>
import baseModal from '@/components/Modal'
import baseTable from '@/components/Table'

export default {
  name: 'App',
  components: {
    baseModal,
    baseTable
  },
  data () {
    return {
      isShowModal: false,
      newUserAdded: false,
      bossesData: [],
      usersData: []
    }
  },
  beforeMount () {
    if (localStorage.getItem('users') && localStorage.getItem('users').length > 0) {
      this.getData()
    }
  },
  methods: {
    isCloseModal () {
      this.isShowModal = false
    },
    addedNewUser ({ name, phone, boss }) {
      this.isShowModal = false
      this.newUserAdded = true
      if (boss) {
        this.usersData = this.findPadawans(this.usersData, name, phone, boss)
      } else {
        this.usersData.push({ name, phone, padawans: [] })
      }
      localStorage.setItem('users', JSON.stringify(this.usersData))
      this.getData()
      setTimeout(() => {
        this.newUserAdded = false
      }, 3600)
    },
    findPadawans (data, userName, userPhone, bossName) {
      const clone = structuredClone(data)
      for (let userKey in clone) {
        if (clone[userKey].name === bossName) {
          clone[userKey].padawans.push({ name: userName, phone: userPhone, padawans: [] })
        } else {
          clone[userKey].padawans = this.findPadawans(clone[userKey].padawans, userName, userPhone, bossName)
        }
      }
      return clone
    },
    getData () {
      this.usersData = JSON.parse(localStorage.getItem('users'))
      this.bossesData = []
      this.getBosses(this.usersData)
    },
    getBosses (data) {
      const clone = structuredClone(data)
      for (let userKey in clone) {
        this.bossesData.push(clone[userKey].name)
        if (clone[userKey].padawans.length > 0) {
          this.getBosses(clone[userKey].padawans)
        }
      }
    }
  }
}
</script>

<style scoped>
#app {
  margin-top: 60px;
}
.surprise {
  width: 550px;
  height: 0;
  transition: 0.2s ease-out;
}
.surprise_active {
  height: 287px;
}

.btn {
  cursor: pointer;
  border-radius: 15px;
  padding: 5px 10px;
  transition: 0.2s ease-out;
}
.btn:hover {
  background-color: #80808070;
}
</style>

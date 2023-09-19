<template>
  <div class="modal">
    <div class="modal__content">
      <div class="modal__head">
        <h3>Добавление пользователя</h3>
        <img
          class="modal__close"
          src="https://img.icons8.com/ios-filled/50/delete-sign--v1.png"
          alt="delete-sign--v1"
          @click="closeModal"/>
      </div>
      <div class="modal__body">
        <div class="body__block">
          <span class="block__label">Имя</span>
          <input
            v-model="name"
            type="text"/>
        </div>
        <div class="body__block">
          <span class="block__label">Телефон</span>
          <input
            v-model="phone"
            type="number"/>
        </div>
        <div class="body__block">
          <span class="block__label">Начальник</span>
          <drop-down
            v-model="boss"
            :bosses="bosses"
            @select="setBoss"/>
        </div>
      </div>
      <div class="modal__footer">
        <button
          class="btn"
          @click="saveData">
          Сохранить
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import dropDown from '@/components/DropDown'

export default {
  name: 'Modal',
  components: {
    dropDown
  },
  data () {
    return {
      name: '',
      phone: '',
      boss: ''
    }
  },
  props: {
    bosses: {
      required: true
    }
  },
  methods: {
    closeModal () {
      this.$emit('close')
    },
    setBoss (value) {
      this.boss = value
    },
    saveData () {
      this.$emit('save', {
        name: this.name,
        phone: this.phone,
        boss: this.boss
      })

      this.name = ''
      this.phone = ''
      this.boss = ''

      this.$emit('close')
    }
  }
}
</script>

<style scoped>
.modal {
  background: rgba(0, 0, 0, 0.8);
  position: fixed;
  top: 0;
  width: 100%;
  height: 100%;
  cursor: pointer;
  /* указываем z-индекс для корректного наслаивания */
  z-index: 1;
}
.modal__content {
  position: absolute;
  width: 350px;
  top: calc(50% - 250px);
  left: calc(50% - 175px);
  border-radius: 10px;
  background-color: rgb(255, 255, 255);
  cursor: default;
  padding: 20px 20px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}
.modal__head {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
}
.modal__close {
  width: 25px;
  height: 25px;
  cursor: pointer;
}
.modal__body {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.body__block {
  display: flex;
  justify-content: space-between;
}
</style>

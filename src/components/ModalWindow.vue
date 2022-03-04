<template>
  <div v-if="show" class="modal-shadow" @click.self="closeModal">
    <div class="modal">
      <div class="modal-close" @click="closeModal">&#10006;</div>
      <h3 class="modal-title">
        <slot name="title">
          Заголовок
        </slot>
      </h3>
      <slot name="body">
        <ul class="errors" v-if="errors.length">
          <li v-for="error in errors" :key="error.id">{{ error }}</li>
        </ul>
        <div class="modal-content">
          <div class="input">
            <input v-model="text" placeholder="quote">
          </div>
          <div class="input">
            <input v-model="author" placeholder="author">
          </div>
          <div class="checkboxes">
            <div class="input">
              <input type="checkbox" id="music" value="music" v-model="tags">
              <label for="music">Музыка</label>
            </div>
            <div class="input">
              <input type="checkbox" id="hobi" value="hobi" v-model="tags">
              <label for="hobi">Хобби</label>
            </div>
            <div class="input">
              <input type="checkbox" id="finances" value="finances" v-model="tags">
              <label for="finances">Финансы</label>
            </div>
            <div class="input">
              <input type="checkbox" id="life" value="life" v-model="tags">
              <label for="life">Жизнь</label>
            </div>
            <div class="input">
              <input type="checkbox" id="auto" value="auto" v-model="tags">
              <label for="auto">Автомобили</label>
            </div>
            <div class="input">
              <input type="checkbox" id="code" value="code" v-model="tags">
              <label for="code">Код</label>
            </div>
            <div class="input">
              <input type="checkbox" id="education" value="education" v-model="tags">
              <label for="education">Учеба</label>
            </div>
            <div class="input">
              <input type="checkbox" id="text" value="text" v-model="tags">
              <label for="text">Текст</label>
            </div>
            <div class="input">
              <input type="checkbox" id="air" value="air" v-model="tags">
              <label for="air">Воздух</label>
            </div>
            <div class="input">
              <input type="checkbox" id="climat" value="climat" v-model="tags">
              <label for="climat">Климат</label>
            </div>
          </div>
        </div>
      </slot>
      <div class="modal-footer">
        <button class="modal-footer__button" @click="sendDataFunction">
          Ок
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ModalWindow',
  data: function () {
    return {
      form: {
        text: '',
        author: '',
        tags: []
      },
      text: '',
      author: '',
      tags: [],
      errors: [],
      show: false
    }
  },
  methods: {
    closeModal: function () {
      this.show = false
    },
    validateData: function () {
      const length = this.tags.length
      this.errors = []
      if (length > 3) {
        this.errors.push('Выберете не более 3 тегов')
      } else if (length < 1) {
        this.errors.push('Выберете хотя бы один тег')
      }
      if (!this.author) {
        this.errors.push('Требуется указать автора')
      }
      if (!this.text) {
        this.errors.push('Требуется ввести текст')
      }
      if (this.errors.length === 0) {
        return true
      }
      return false
    },
    sendDataFunction: async function () {
      if (this.validateData()) {
        await axios.post('http:127.0.0.1:8000/api/news', this.form).catch(err => console.log(err))
        this.closeModal()
      }
      return false
    }
  }
}
</script>

<style scoped>
.modal-shadow {
  position: fixed;
  top: 0;
  left: 0;
  min-height: 100%;
  width: 100%;
  background: rgba(0, 0, 0, 0.39);
}
.errors li{
  list-style-type: none;
  color: #842029;
}
.modal {
  background: #fff;
  border-radius: 8px;
  padding: 15px;
  min-width: 300px;
  max-width: 480px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.modal-close {
   float: right;
   border-radius: 50%;
   color: #fff;
   background: #517AA3;
   display: flex;
   align-items: center;
   justify-content: center;
   position: absolute;
   top: 7px;
   right: 7px;
   width: 30px;
   height: 30px;
   cursor: pointer;
 }

.modal-title {
   color: #517AA3;
 }

.modal-content {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: center;
}

input {
  padding: 5px;
  border: solid 1px #333;
  margin: 10px 5px;
}

.input {
  margin-right: 8px;
  display: flex;
  align-items: center;
}

.modal-footer__button {
   background-color: #517AA3;
   color: #fff;
   border: none;
   text-align: center;
   padding: 8px;
   font-size: 17px;
   font-weight: 500;
   border-radius: 8px;
   min-width: 150px;
 }

.checkboxes {
  display: flex;
  flex-wrap: wrap;
}
@media (max-width:426px) {
.modal-content {
   align-items: center;
 }
.modal-footer {
   text-align: center;
 }
}
</style>

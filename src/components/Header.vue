<template>
  <div>
  <header class="d-flex justify-content-center py-3">
    <ul class="nav nav-pills">
      <li class="nav-item add-quote"><a href="#" class="nav-link" aria-current="page" @click="showModal">Добавить цитату</a></li>
    </ul>
  </header>
  <modal-window ref="modal"></modal-window>
  </div>
</template>

<script>

import ModalWindow from './ModalWindow'

export default {
  name: 'Header',
  components: { ModalWindow },
  methods: {
    showModal: function () {
      this.$refs.modal.show = true
    }
  }
}
</script>

<style scoped>
header{
  display: flex;
  justify-content: center;
  background-color: #F8F9FA;
  border-bottom: solid 1px #333;
  padding-top: 1rem;
  padding-bottom: 1rem;
}
.nav{
  margin-top: 0;
  display: flex;
  flex-wrap: wrap;
  padding-left: 0;
  margin-bottom: 0;
  list-style: none;
}
.add-quote{
  border-radius: 5px;
  background-color: #517AA3;
}
.nav-link{
  display: block;
  padding: 0.5rem 1rem;
  text-decoration: none;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out, border-color 0.15s ease-in-out;
  color: #FBFCFD;
  background: none;
  border: 0;
  border-radius: 0.25rem;
}
</style>

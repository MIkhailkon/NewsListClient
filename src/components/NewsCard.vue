<template>
  <div class="row">
    <div class="col-md-8 col-md-offset-2">
      <div class="panel panel-default">
        <div class="text">
          <slot name="text">
            Текст Цитаты
          </slot>
        </div>
        <h3 class="author">
          <slot name="author">
            Автор
          </slot>
        </h3>
        <div class="tags">
          <slot name="tag"></slot>
        </div>
        <h3 class="created">
          <slot name="created">
            15.02.2000
          </slot>
        </h3>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  mounted () {
  }
}
</script>

<style scoped>
.row {
  --bs-gutter-x: 1.5rem;
  --bs-gutter-y: 0;
  display: flex;
  flex-wrap: wrap;
}
.tags {
  color: rgb(0, 55, 107);
  max-width: 240px;
  display: flex;
  justify-content: flex-start;
}
.author {
  font-size: 15px;
}

.created {
  padding: 5px;
  font-size: 13px;
}
.text{
  font-size: 22px;
}

@media (max-width: 425px) {
  .text{
    font-size: 18px;
  }
}
</style>

<template>
  <div>
    <div class="pagination-block">
      <div class="pagination-block__page"
           :class="[
             settings.pageClass
           ]"
      >
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PaginationPage',
  props: ['settings']
}
</script>

<style scoped>
  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
</style>

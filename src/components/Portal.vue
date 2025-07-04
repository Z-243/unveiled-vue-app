<script setup>
defineProps({
  showModal: Boolean,
  handleCloseModal: Function,
});
</script>

<template>
  <!--use v-if="" to conditional render  -->
  <Teleport v-if="showModal" to="#portal">
    <div class="portal-container">
      <!-- to turn this div to button we need to give it a role, so we can click out of the div -->
      <div
        class="portal-underlay"
        role="button"
        tabindex="0"
        @click="handleCloseModal"
      ></div>
      <div class="portal-content">
        <slot />
      </div>
    </div>
  </Teleport>
</template>

<style scoped></style>

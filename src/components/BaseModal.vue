<template>
  <div
    v-show="modalActive"
    class="absolute w-full bg-black bg-opacity-30 h-screen top-0 left-0 flex justify-center px-8"
  >
    <div v-if="modalActive" class="bg-white self-start mt-52 max-w-screen-md min-w-96">
      <div class="bg-black text-white text-sm px-2">{{ props.modalTitle }}</div>
      <div class="p-2 text-lg">
        <slot />
      </div>
      <div class="flex justify-between">
        <button @click="emit('close-modal')" class="btn">Закрыть</button>
        <button @click="emit('select-folder')" class="btn">Ок</button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const emit = defineEmits(['close-modal', 'select-folder'])
const props = defineProps({
  modalActive: {
    type: Boolean,
    default: false,
  },
  modalTitle: {
    type: String,
    default: 'Title',
  },
})
</script>

<style scoped>
.btn {
  @apply text-white mt-8 py-2 px-6 bg-black;
}
</style>

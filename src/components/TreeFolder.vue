<template>
  <div class="">
    <button @click="toggleModal" class="border-4 border-black p-5 rounded-xl">
      Open Tree Folder
    </button>
  </div>
  <BaseModal
    modalTitle="Tree Folder"
    :modalActive="modalActive"
    @close-modal="toggleModal"
    @select-folder="handleSelect"
  >
    <TreeItem
      v-for="item in folderTree"
      :id="item.id"
      :key="item.id"
      :name="item.name"
      :depth="0"
      :data="item.children"
      @select="selectFolder"
    />
  </BaseModal>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import BaseModal from './BaseModal.vue'
import TreeItem from './TreeItem.vue'
import type { TreeItem as TreeItemType } from '@/types/TreeItem'

const folderTree = ref<TreeItemType[]>([
  {
    id: 1,
    name: 'Папка 1',
    children: [
      { id: 2, name: 'Папка 1.1', children: [] },
      { id: 3, name: 'Папка 1.2', children: [{ id: 4, name: 'Папка 1.2.1', children: [] }] },
    ],
  },
  { id: 5, name: 'Папка 2', children: [] },
])

const modalActive = ref<boolean>(false)
const toggleModal = () => {
  modalActive.value = !modalActive.value
}

const selectedFolder = ref<null | string>(null)

const selectFolder = (id: string) => {
  selectedFolder.value = id
}

const handleSelect = () => {
  if (!selectedFolder.value) {
    console.log('Вы не выбрали папку')
  } else {
    console.log('ID выбранной папки:', selectedFolder.value)
  }
  toggleModal()
}
</script>

<style scoped></style>

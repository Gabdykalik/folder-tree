<template>
  <div @click="handleSelect" class="label max-w-max cursor-pointer">{{ name }}</div>
  <div v-show="showChildren" class="ml-3">
    <tree-item
      v-for="(item, index) in data"
      :id="item.id"
      :key="index"
      :name="item.name"
      :depth="depth + 1"
      :data="item.children"
      @select="$emit('select', $event)"
    />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { TreeItem as TreeItemType } from '@/types/TreeItem'

const props = defineProps<{
  id: number
  name: string
  depth: number
  data: TreeItemType[]
}>()

const emit = defineEmits(['select'])

const showChildren = ref(false)

const handleSelect = () => {
  emit('select', props.id)
  showChildren.value = !showChildren.value
}
</script>

<style scoped></style>

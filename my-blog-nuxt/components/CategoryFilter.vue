<template>
  <div>
    <select :value="modelValue" @change="$emit('update:modelValue', $event.target.value)">
      <option value="">All Categories</option>
      <option v-for="cat in categories" :key="cat" :value="cat">
        {{ cat }}
      </option>
    </select>
  </div>
</template>

<script setup>
defineProps({
  categories: {
    type: Array,
    required: true
  },
  modelValue: {
    type: String,
    default: ''
  }
})

defineEmits(['update:modelValue'])
</script>

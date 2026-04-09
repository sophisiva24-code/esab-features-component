<template>
  <div class="dropdown" ref="dropdownRef">
    
    <!-- Trigger -->
    <div class="dropdown-trigger" @click="toggle">
      <span :class="{ 'placeholder': !modelValue }">
        {{ selectedLabel || placeholder }}
      </span>
      <span class="arrow">&#8964;</span>
    </div>

    <!-- Options -->
    <div v-if="isOpen" class="dropdown-menu">
      <div
        v-for="option in options"
        :key="option.value"
        class="dropdown-item"
        :class="{ active: option.value === modelValue }"
        @click="select(option)"
      >
        {{ option.label }}
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount, defineProps, defineEmits } from 'vue'

const props = defineProps({
  modelValue: [String, Number],
  options: {
    type: Array,
    default: () => []
  },
  placeholder: {
    type: String,
    default: 'Select an option'
  }
})

const emit = defineEmits(['update:modelValue'])

const isOpen = ref(false)
const dropdownRef = ref(null)

const toggle = () => {
  isOpen.value = !isOpen.value
}

const select = (option) => {
  emit('update:modelValue', option.value)
  isOpen.value = false
}

const selectedLabel = computed(() => {
  return props.options.find(o => o.value === props.modelValue)?.label
})

// Close on outside click
const handleClickOutside = (e) => {
  if (!dropdownRef.value?.contains(e.target)) {
    isOpen.value = false
  }
}

onMounted(() => {
  document.addEventListener('click', handleClickOutside)
})

onBeforeUnmount(() => {
  document.removeEventListener('click', handleClickOutside)
})
</script>

<style scoped lang="scss">
@use '../../styles/_variables' as *;

.dropdown {
  position: relative;
}

.dropdown-trigger {
  border: 1px solid $esab-gray-2;
  padding: 10px;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  border-radius: $radius;
}

.placeholder {
  color: $esab-gray-3;
}

.dropdown-menu {
  position: absolute;
  width: 100%;
  border: 1px solid $esab-gray-2;
  background: $esab-white;
  z-index: 10;
  margin-top: 4px;
  border-radius: $radius;
}

.dropdown-item {
  padding: 10px;
  cursor: pointer;
}

.dropdown-item:hover {
  background: $esab-yellow;
}

.dropdown-item.active {
  background: $primary-color;
}

.arrow {
  margin-top: -$sp-1;
  font-size: $sp-3;
}
</style>
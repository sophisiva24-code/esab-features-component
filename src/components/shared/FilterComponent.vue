<template>
  <div class="filter-tabs">
    <button
      v-for="category in categories"
      :key="category.id"
      :class="['filter-tabs__btn', { active: activeId === category.id }]"
      @click="selectCategory(category.id)"
    >
      {{ category.name }}
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { defineEmits, defineProps } from 'vue';

const props = defineProps({
  categories: {
    type: Array,
    required: true
  },
  activeCategory: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['change'])

const activeId = ref(props.activeCategory)

const selectCategory = (id) => {
  activeId.value = id
  emit('change', id)
}

</script>

<style lang="scss" scoped>
@use '../../styles/_variables' as *;

.filter-tabs {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
  
  &__btn {   
    padding: $sp-1 $sp-3;
    border-radius: $sp-5;
    border: 1px solid $border;
    background: transparent;
    font-family: $font-family;
    font-size: $ft-14;
    font-weight: $fw-medium;
    color: $text-muted;
    cursor: pointer;
    border: 1px solid $border;
    background: transparent;   

    &:hover, &.active {
        background: $esab-black;
        color: $esab-white;
        border-color: $esab-black;
    }
  }
}
</style>
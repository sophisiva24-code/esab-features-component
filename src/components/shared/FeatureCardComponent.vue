<template>
  <div class="card" @click="toggleCard">
    <p class="card__category">{{ card.category }}</p>
      <div class="card__image-wrapper">
      <img 
        src="@/assets/images/ESAB_Ruffian_EMP_270G_EDW_Environment_Action_hi_14.webp" 
        alt="feature image"
        class="card__image"  
        width="500"
        height="300"
        loading="lazy"/>
    </div>

    <div class="card__icon">
      <img src="@/assets/icons/power.svg" alt="" />
    </div>

    <div class="card__title-row" @click="toggleCard">
      <h3 class="card__title">{{ card.title }}</h3>
    </div>

    <p class="card__description"
      :class="{ collapsed: !isExpanded }">
      {{ card.description }}
    </p>
  </div>

</template>

<script setup>
import { defineProps,ref } from 'vue';

defineProps({
  card: {
    type: Object,
    required: true
  }
})

const isExpanded = ref(false)

const toggleCard = () => {
  isExpanded.value = !isExpanded.value
}
</script>

<style lang="scss" scoped>
@use '@/styles/variables' as *;

.card {
  background: $surface-alt;
  border-radius: 12px;
  padding: $sp-3;
  border: 1px solid $border;
  min-height: 300px;
  display: flex;
  flex-direction: column;
  height: 100%;

  &__category {
    font-size: $ft-12;
    letter-spacing: 1px;
    margin-bottom: 12px;
    font-weight: $fw-bold;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: $text-muted;
    margin-bottom: $sp-1;
  }
  &__image-wrapper {
    width: 100%;
    height: 150px;
    overflow: hidden;
    border-radius: $radius-lg;
  }
  &__image {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
  &__icon {
    border: 2px dashed $border;
    border-radius: 10px;
    padding: $sp-1;
    text-align: center;
    position: relative;
    margin: 10px 0;
    width: 48px;
    height: 48px;
    display: flex;
  }

  &__title {
    font-size: 20px;
    font-weight: $fw-bold;
    margin-bottom: 10px;
  }

  &__description {
    color: $text-muted;
    line-height: 1.5;
    font-size: $ft-14;
    transition: all 0.3s ease;
  }
  &__description.collapsed {
    display: -webkit-box;
    -webkit-line-clamp: 2;
    line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
    cursor: pointer;
  }
  &:hover {
    box-shadow: 0 0 0 2px $esab-yellow;
    background-color: $esab-white;
  }
}

.card__title-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

</style>
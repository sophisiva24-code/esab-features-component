<template>
  <div class="slider">
    <button class="slider-arrow prev" @click="previous" :disabled="currentIndex === 0">
      &#8592;
    </button>

    <div class="slider__viewport">
      <div
        class="slider__track"
        :style="{ transform: `translateX(-${currentIndex * cardWidth}%)` }"
      >
        <div
          class="slider__card"
          v-for="card in cards"
          :key="card.id"
        > 
          <FeatureCardComponent :card="card" :key="card.id"/>
        </div>
      </div>
    </div>

    <button class="slider-arrow next" @click="next" :disabled="end === props.cards.length">
      &#8594;
    </button>
  </div>
  <div class="slider-counter">
    Showing {{ start }}–{{ end }} of {{ props.cards.length }} features
  </div>
</template>

<script setup>
import { ref, computed, onMounted, defineProps, watch } from 'vue'
import FeatureCardComponent from './FeatureCardComponent.vue'

const props = defineProps({
  cards: Array
})
// whenever there is a change in the cards prop, reset the slider to the first position
watch(() => props.cards, () => {
  currentIndex.value = 0
})

const currentIndex = ref(0)
const visibleCards = ref(4)

const updateVisibleCards = () => {
  if (window.innerWidth < 768) visibleCards.value = 1
  else if (window.innerWidth < 1024) visibleCards.value = 2
  else visibleCards.value = 4
}

onMounted(() => {
  updateVisibleCards()
  window.addEventListener('resize', updateVisibleCards)
})

const cardWidth = computed(() => 100 / visibleCards.value)

const next = () => {
  if (currentIndex.value < props.cards.length - visibleCards.value) {
    currentIndex.value++
  }
}

const previous = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--
  }
}
const start = computed(() => currentIndex.value + 1)
const end = computed(() =>
  Math.min(currentIndex.value + visibleCards.value, props.cards.length)
)
</script>
<style lang="scss" scoped>
@use '../../styles/_variables.scss' as *;
.slider {
  position: relative;
  display: flex;
  align-items: center;

  .slider-arrow {
    background: $esab-white;
    border: none;
    padding: $sp-1;
    border-radius: 50%;
    border: 1px solid $border;
    transform: translateY(-50%);
    width: 44px;
    height: 44px;
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 18px;
    z-index: 10;
    box-shadow: 0 2px $sp-1 rgba($esab-black, 0.1);
    color: $text;
    cursor: pointer;
  }

  .slider-arrow:disabled {
    opacity: 0.3;
    cursor: not-allowed;
  }

  .prev {
    left: -22px;
  }

  .next {
    right: -22px;
  }

  &__viewport {
    overflow: hidden;
    width: 100%;
  }

  &__track {
    display: flex;
    gap: 0px;
    transition: transform 0.4s ease-in-out;
  }

  &__card {
    flex: 0 0 calc(100% / 4); // default desktop
    padding: $sp-2;
    box-sizing: border-box;
  }
}
.slider-counter {
  text-align: center;
  margin-top: $sp-2;
  font-size: $ft-14;
  color: $text-muted;
  font-weight: $fw-medium;
}

/* Responsive */
@media (max-width: 1024px) {
  .slider__card {
    flex: 0 0 calc(100% / 2);
  }
}

@media (max-width: 768px) {
  .slider__card {
    flex: 0 0 100%;
  }
}
</style>
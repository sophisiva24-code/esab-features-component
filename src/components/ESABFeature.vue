<template>
    <HeaderComponent @navigate="scrollToSection" />
  <main>
     <WeldingEquipmentComponent />
  </main>
</template>

<script setup>
import HeaderComponent from './HeaderComponent.vue';
import WeldingEquipmentComponent from './WeldingEquipmentComponent.vue';

const scrollToSection = (id) => {
  const el = document.getElementById(id)
  const offset = 80;
  if (el) {
    const top = el.offsetTop - offset
    el.scrollIntoView({ top, behavior: 'smooth' })
  }
}
</script>
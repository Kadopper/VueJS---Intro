<script setup>
import { ref, onMounted } from 'vue';

const mouseX = ref(0);
const mouseY = ref(0);
const showMenu = ref(false); 
const radius = 100

function showPosition(event) {
  mouseX.value = event.clientX;
  mouseY.value = event.clientY;
  showMenu.value = !showMenu.value;
}

onMounted(() => {
  window.addEventListener('click', showPosition);
});

</script>

<template>
  <div>
    <p>X: {{ mouseX }}</p>
    <p>Y: {{ mouseY }}</p>

    <div 
      v-if="showMenu" 
      :style="{ top: `${mouseY-radius}px`, left: `${mouseX}px` }" 
      class="menuBox">
    </div>

  </div>
</template>

<style scoped>
.menuBox {
  width: 50px;
  height: 50px;
  background-color: red;
  position: absolute;
  transform: translate(-50%, -50%);
  border-radius: 50% 
}
</style>

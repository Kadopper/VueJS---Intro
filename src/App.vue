<script setup>
import { ref, onMounted } from 'vue';

// variables for mouse X/Y 
const mouseX = ref(0);
const mouseY = ref(0);
const showSquare = ref(false); // Control the visibility of the square

// Function to update mouse position and show the square
function showPosition(event) {
  mouseX.value = event.clientX;
  mouseY.value = event.clientY;
  showSquare.value = true; // Make the square appear on click
}

// eventListener
onMounted(() => {
  window.addEventListener('click', showPosition);
});
</script>

<template>
  <div>
    <p>X: {{ mouseX }}</p>
    <p>Y: {{ mouseY }}</p>

    <!-- Red square that appears on click -->
    <div 
      v-if="showSquare" 
      :style="{ top: `${mouseY}px`, left: `${mouseX}px` }" 
      class="red-square">
    </div>
  </div>
</template>

<style scoped>
.red-square {
  width: 20px;
  height: 20px;
  background-color: red;
  position: absolute;
  transform: translate(-50%, -50%); /* Center the square on the click */
}
</style>

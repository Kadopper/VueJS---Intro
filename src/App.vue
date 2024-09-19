<script setup>
import { ref, onMounted } from 'vue';

const mouseX = ref(0);
const mouseY = ref(0);
const showMenu = ref(false); 
const radius = 100;
const numberOfItems = 4
const angleCircle= 360/numberOfItems

function showPosition(event) {
  mouseX.value = event.clientX;
  mouseY.value = event.clientY;
  showMenu.value = !showMenu.value;
}

function showAlert(event){
  alert("yo")
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
      @click.stop="showAlert"
      :style="{ 
        left: `${mouseX}px`, 
        top: `${mouseY}px`
        }" 
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
  border-radius: 50%;
  cursor: pointer;
}
</style>

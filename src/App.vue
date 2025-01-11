<script setup>
import { ref, computed } from 'vue';

// changeable variables for posistion
const mouseX = ref(0);
const mouseY = ref(0);

// boolean of the menu visibility: 
const showMenu = ref(false);

// how far from the mouse the menus should be and the number of menus 
const radius = 100;
const numberOfItems = ref(10);

// Calculate the angle for menu items dynamically based on `numberOfItems`
const anglesOfCircle = computed(() => (2 * Math.PI) / numberOfItems.value);

// when loaded, it add an event listener that open the menu when you click anywhere in the window
window.addEventListener('click', updateMenu);

// updates the loaction of the mouse, and the boolean for the menu 
function updateMenu(event) {
  mouseX.value = event.clientX;
  mouseY.value = event.clientY;
  showMenu.value = !showMenu.value;
}

// Prevent menu toggle when clicking on specific elements (LÆS OP)
function preventMenu(event) {
  event.stopPropagation();
}

// display which option was clicked on, every alert uses its index as an argument
function showAlert(menuIndex) {
  alert(`This is menu ${menuIndex}`);
}
</script>

<template>
  <label @click="preventMenu">
    Number of Menus:
    <input type="number" v-model="numberOfItems" min="1" @click="preventMenu" />
  </label>

  <!-- if the showMenu boolean is true, display the menu -->
  <div v-if="showMenu">

    <!-- using v-for, i can render multiple elemetns, wherein i calculate each position in a circle. Furthermore i give it teh ability to show an alert for each menu clicked. -->
    <div v-for="menuIndex in numberOfItems" :style="{
    left: `${mouseX + radius * Math.cos(anglesOfCircle * menuIndex)}px`,
    top: `${mouseY + radius * Math.sin(anglesOfCircle * menuIndex)}px`,
    transform: 'translate(-50%, -50%)'
    }" class="menu" @click="showAlert(menuIndex)">
      <!-- display the menu index of each menu -->
      Menu: {{ menuIndex }}
    </div>

  </div>
  
</template>

<style scoped>
.menu {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: blue;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  cursor: pointer;
  color: white;
  font-size: 12px;
}
</style>

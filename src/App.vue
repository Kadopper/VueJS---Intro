<script setup>
import { ref } from 'vue';

// changeable reactive variables for posistion
const mouseX = ref(0);
const mouseY = ref(0); 
const toggleMenu = ref(false);
const radiusOfMenu = 100;

// Calculate the angle for menu items dynamically based on `numberOfMenus`
const numberOfMenus = ref(10);
const anglesOfCircle = ref((2 * Math.PI) / numberOfMenus.value)

function updateAngleOfCircle(){
  anglesOfCircle.value = (2 * Math.PI) / numberOfMenus.value;
}

// updates the loaction of the mouse, and the boolean for the menu 
// when a mouse events happen
function updateMenu(event) {
  mouseX.value = event.clientX;
  mouseY.value = event.clientY;
  toggleMenu.value = !toggleMenu.value;
}

// it adds an event listener that open the menu when you click anywhere in the window
window.addEventListener('click', updateMenu);

// Prevent menu toggle when clicking on specific elements (LÆS OP)
function preventMenu(event) {
  event.stopPropagation();
}

// display which option was clicked on, every alert uses its index as an argument
function showAlert(menuIndex) {
  alert(`This is menu ${menuIndex}`)
}

</script>

<template>
  <!-- stops the menu from opening if it the div is clicked-->
  <div @click="preventMenu">
    Number of Menus:
    <input type="number" v-model="numberOfMenus" @input="updateAngleOfCircle" />
  </div>

  <!-- if the toggleMenu boolean is true, display the div / menu -->
  <div v-if="toggleMenu">
    <!-- using v-for, i can render multiple elemetns, wherein i calculate each position in a circle. Furthermore i give it teh ability to show an alert for each menu clicked. -->
    <div v-for="menuIndex in numberOfMenus"
    :style="
    {
    left: `${mouseX + radiusOfMenu * Math.cos(anglesOfCircle * menuIndex)}px`,
    top: `${mouseY + radiusOfMenu * Math.sin(anglesOfCircle * menuIndex)}px`,
    transform: 'translate(-50%, -50%)'
    } 
    "class="menu" @click="showAlert(menuIndex)">
      <!-- display the menu index of each menu -->
      Menu: {{ menuIndex }}
    </div>

  </div>
  
</template>

<style>
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

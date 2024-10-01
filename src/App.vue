<script setup>
import { ref, onMounted } from 'vue';

// changeable variables
const mouseX = ref(0);
const mouseY = ref(0);
const showMenu = ref(false); 

// how far from the mouse the menus should be, the number of item (menus) and calcuates teh angle
const radius = 100;
// is changeable yippie!!!1
const numberOfItems = 6
const anglesOfCircle = ((2*Math.PI)/numberOfItems)

// when loaded, it add an event listener that open the menu when you click anywhere in the window
onMounted(() => {
  window.addEventListener('click', showPosition);
});

// updates the loaction of the mouse, and the boolean for the menu 
function showPosition(event) {
  mouseX.value = event.clientX;
  mouseY.value = event.clientY;
  showMenu.value = !showMenu.value;
}


// display which option was clicked on, every alert uses its index as an argument
function showAlert(menuIndex) {
  alert(`This is menu ${menuIndex}`);
}
</script>

<template>
  <div>
    <div>
      <!-- display mouse position when window is clicked-->
    <p>X: {{ mouseX }}</p>
    <p>Y: {{ mouseY }}</p>

      <!-- if the showMenu boolean is true, display the menu -->
    <div 
      v-if="showMenu" 
    >
      <!-- using v-for, i can render multiple elemetns, wherein i calculate each position in a circle. Furthermore i give it teh ability to show an alert for each menu clicked. -->
      <div
        v-for="menuIndex in numberOfItems" 
        :style="{
          left: `${mouseX + radius * Math.cos(anglesOfCircle * menuIndex)}px`,
          top: `${mouseY + radius * Math.sin(anglesOfCircle * menuIndex)}px`,
          transform: 'translate(-50%, -50%)'
        }"
        class="menu"
        @click="showAlert(menuIndex)"
      >
        Menu: {{ menuIndex }}
      </div>
    </div>
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

<script setup>
import { ref } from 'vue'; // Import the 'ref' function from Vue to create reactive references

const mouseX = ref(0);
const mouseY = ref(0);
// Reactive reference to store the message text

export defualt{
  data(){
    return{
      function showAlert(event) {
        mouseX.value = client.eventX;
        mouseY.value = client.eventY;
      }
    }
  }
}
</script>

<template>
  <!-- Display the current message -->
  <div class="background" @mouseClick="showAlert">
    <p>{{ mouseX }}</p>
    <p>{{ mouseY }}</p>
  </div>
</template>

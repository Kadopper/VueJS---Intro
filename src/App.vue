<script setup>
import { ref } from 'vue';
import { reactive } from 'vue';

const pepita = reactive({
  energy: ref(100)
})

const gToEat = ref(0)
const kmsToFly = ref(0)

export default{
  data(){
    return{
const mouseX = ref(0);
const mouseY = ref(0);
    }
  }
}
// Reactive reference to store the message text


 function showAlert() {
  mouseX.value = client.eventX;
  mouseY.value = client.eventY;
 }

</script>

<template>
  <!-- Display the current message -->
  <div class="background" @mouseClick="showAlert">
    <p>{{ mouseX }}</p>
    <p>{{ mouseY }}</p>
  </div>
</template>

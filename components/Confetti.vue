<script setup lang="ts">
import confetti from 'canvas-confetti';
import { onMounted } from 'vue'

const defaults = {
    spread: 360,
    ticks: 50,
    gravity: 0,
    decay: 0.94,
    startVelocity: 30,
    shapes: ['star'],
    colors: ['FFE400', 'FFBD00', 'E89400', 'FFCA6C', 'FDFFB8']
  };
  
 function shoot() {
    confetti({
      ...defaults,
      particleCount: 40,
      scalar: 1.2,
      shapes: ['star']
    });
  
    confetti({
      ...defaults,
      particleCount: 10,
      scalar: 0.75,
      shapes: ['circle']
    });
  }

onMounted(() => {
  setTimeout(shoot, 0);
  setTimeout(shoot, 400);
  setTimeout(shoot, 800);
})
</script>

<template>

</template>

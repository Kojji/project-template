<script setup>
import { ref } from 'vue'

const msg = import.meta.env.VITE_MESSAGE

</script>
<template>
  <div>
    <h1>About</h1>
    <p>{{msg}}</p>
  </div>
</template>

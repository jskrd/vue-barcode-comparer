<template>
  <div class="container my-4">
    <BarcodeComparer></BarcodeComparer>
  </div>
</template>

<script>
import BarcodeComparer from './components/BarcodeComparer.vue'

export default {
  name: 'app',
  components: {
    BarcodeComparer
  }
}
</script>

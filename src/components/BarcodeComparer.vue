<template>
  <div>
    <p class="text-center mb-5">
      <button class="btn btn-secondary btn-lg" v-on:click="clear()">Clear</button>
    </p>
    <div class="row">
      <div class="col-6">
        <Card title="Covers" :barcodes="covers" :comparedBarcodes="inners"></Card>
      </div>
      <div class="col-6">
        <Card title="Inners" :barcodes="inners" :comparedBarcodes="covers"></Card>
      </div>
    </div>
  </div>
</template>

<script>
import Card from './BarcodeComparerCard.vue'

export default {
  name: 'BarcodeComparer',
  components: {
    Card
  },
  data: function () {
    return {
      covers: [],
      inners: []
    }
  },
  methods: {
    clear: function () {
      this.covers = []
      this.inners = []
    }
  }
}
</script>

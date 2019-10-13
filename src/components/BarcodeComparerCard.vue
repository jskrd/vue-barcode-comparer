<template>
  <div class="card">
    <div class="card-body">
      <h4 class="card-title text-center">
        <a href="#" class="text-dark stretched-link" v-on:click="$refs.barcode.focus()">{{ title }}</a>
      </h4>
      <table class="table table-sm text-monospace small">
        <col width="20%">
        <col width="80%">
        <tbody>
          <tr v-for="(barcode, index) in barcodes" :key="index" :class="context(index)">
            <th scope="row">{{ index + 1 }}</th>
            <td>{{ barcode }}</td>
          </tr>
        </tbody>
      </table>
      <form v-on:submit.prevent="append">
        <input :id="title" type="text" class="form-control" placeholder="Scan barcode" ref="barcode">
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BarcodeComparerCard',
  props: {
    title: String,
    barcodes: Array,
    comparedBarcodes: Array
  },
  methods: {
    context: function (index) {
      return {
        'table-success': this.matches(index) === true,
        'table-danger': this.matches(index) === false
      }
    },
    matches: function (index) {
      if (this.barcodes[index] === this.comparedBarcodes[index])
        return true

      if (this.comparedBarcodes.includes(this.barcodes[index]))
        return false

      return null
    },
    append: function () {
      this.barcodes.push(this.$refs.barcode.value)
      this.$refs.barcode.value = ''
    }
  }
}
</script>

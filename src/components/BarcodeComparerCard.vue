<template>
  <div class="card">
    <div class="card-body">
      <h4 class="card-title text-center mb-3">
        <a href="#" class="text-dark stretched-link" v-on:click="$refs.barcode.focus()">{{ title }}</a>
      </h4>
      <table class="table table-sm text-monospace small">
        <tbody>
          <tr v-for="(barcode, index) in barcodes" :key="index" :class="context(index)">
            <th scope="row" class="text-right">{{ index + 1 }}</th>
            <td class="w-100 text-center">
              {{ barcode }}
              <span v-if="matches(index) === false">
                (matches with {{ matchesWith }} {{ comparedBarcodes.indexOf(barcode) + 1 }})
              </span>
            </td>
          </tr>
        </tbody>
      </table>
      <form v-on:submit.prevent="append">
        <div class="input-group">
          <div class="input-group-prepend">
            <span class="input-group-text"><i class="fas fa-barcode"></i></span>
          </div>
          <input :id="title" type="text" class="form-control" placeholder="Scan barcode" ref="barcode">
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BarcodeComparerCard',
  props: {
    title: String,
    matchesWith: String,
    barcodes: Array,
    comparedBarcodes: Array
  },
  methods: {
    context: function (index) {
      return {
        'bg-success text-white': this.matches(index) === true,
        'bg-warning': this.matches(index) === false,
        'bg-danger text-white': this.matches(index) === null
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

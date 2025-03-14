
<template>
  <div class="col-lg-12">
    <div ref="tableContainer" class="table-container">
      <div class="table-wrapper">
        <table class="table table-dark table-striped responsive-table">
          <thead class="table-header">
            <tr>
              <th class="text-center">#</th>
              <th class="text-center" v-for="header in tableData.headers" :key="header">{{ header }}</th>
            </tr>
          </thead>
          <tbody class="table-body">
            <tr v-for="(row, rowIndex) in tableData.rows" :key="rowIndex">
              <td class="text-center">{{ rowIndex + 1 }}</td>
              <td v-for="header in tableData.headers" :key="header" :class="{'text-end': isCurrency(header), 'text-center': isCenter(header)}">
                <IncrementDecrement v-if="header === 'QUANTITY'" v-model="row[header]" />
                <span v-else>{{ row[header] }}</span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import IncrementDecrement from './IncrementDecrement.vue';

const containerHeight = ref(window.innerHeight);

const tableData = ref({
  headers: [ "ITEM NAME", "QUANTITY", "PRICE", "DISCOUNT", "TAX", "TOTAL"],
  rows: [
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    { "ITEM NAME": "Item A", "QUANTITY": 1, "PRICE": 100, "DISCOUNT": 5, "TAX": 10, "TOTAL": "Rp500.000" },
    { "ITEM NAME": "Item B", "QUANTITY": 1, "PRICE": 200, "DISCOUNT": 10, "TAX": 20, "TOTAL": "Rp1.500.000" },
    // Add more rows as needed
  ]
});

const isCurrency = (header) => {
  return ["PRICE", "DISCOUNT", "TAX", "TOTAL"].includes(header);
};

const isCenter = (header) => {
  return ["QUANTITY"].includes(header);
};

const updateDimensions = () => {
  containerHeight.value = window.innerHeight;
};

onMounted(() => {
  window.addEventListener('resize', updateDimensions);
  updateDimensions(); // Call it once initially to set the correct height
});

onUnmounted(() => {
  window.removeEventListener('resize', updateDimensions);
});
</script>

<style scoped>
.table-container {
  /* height: calc(63vh); Set height to 80% of the viewport height */
  overflow-y: auto; /* Enable vertical scrolling */
}

.table-wrapper {
  display: block;
}

.table {
  width: 100%;
  table-layout: fixed;
}

.table-header {
  display: table;
  width: 100%;
  table-layout: fixed;
  background-color: #343a40;
  position: sticky;
  top: 0; /* Keep the header at the top */
}

.table-body {
  display: block;
  max-height: calc(65vh - 60px); /* Adjust height to keep the header in view */
  overflow-y: auto;
}

.table-body tr {
  display: table;
  width: 100%;
  table-layout: fixed;
}

.table-body td, .table-header th {
  padding: 8px;
  text-align: left;
  vertical-align: top;
  border-top: 1px solid #dee2e6;
}
</style>
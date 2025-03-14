<script setup>
import Content from "./Content.vue"
import Sidebar from "./Sidebar.vue"
import TotalHeader from "./TotalHeader.vue"
import SalesBar from "./SalesBar.vue"
import Table from "./Table.vue"
</script>

<template>
  <div>
    <div class="row m-2">
      <div class="col-lg-12">
        <div class="row justify-content-between">
          <div class="col-lg-3 d-flex align-items-center">
            <img src="assets/img/logo-cashier.png" width="120" class="rounded" alt="Logo">
          </div>
          <div class="col-lg-6">
            <TotalHeader />
          </div>
          <div class="col-lg-3">
            <Sidebar />
          </div>
        </div>
        <SalesBar />
      </div>
      <div class="row pr-1">
        <Table />
      </div>
    </div>
  </div>
</template>

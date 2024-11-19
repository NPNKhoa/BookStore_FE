<template>
  <div>
    <p-dataTable
      :value="rows"
      :paginator="pagination"
      :rows="rowsPerPage"
      :sortable="sortable"
      :filterable="filterable"
      :striped-rows="true"
      :size="tableSize"
      :rows-per-page-options="[5, 10, 20]"
    >
      <template v-for="column in columns" :key="column.field">
        <p-column
          :field="column.field"
          :header="column.header"
          :sortable="column.sortable || false"
          :filter="column.filter || false"
        ></p-column>
      </template>
    </p-dataTable>
  </div>
</template>

<script>
import DataTable from "primevue/datatable";
import Column from "primevue/column";

export default {
  name: "DataTable",
  components: {
    "p-dataTable": DataTable,
    "p-column": Column,
  },
  props: {
    rows: {
      type: Array,
      required: true,
    },
    columns: {
      type: Array,
      required: true,
    },
    sortable: {
      type: Boolean,
      default: false,
    },
    filterable: {
      type: Boolean,
      default: false,
    },
    pagination: {
      type: Boolean,
      default: false,
    },
    rowsPerPage: {
      type: Number,
      default: 10,
    },
  },
  data() {
    return {
      tableSize: "large",
    };
  },
};
</script>

<style></style>

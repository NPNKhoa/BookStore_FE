<template>
  <div class="flex">
    <!-- Sidebar -->
    <Sidebar />

    <!-- Main content -->
    <main class="flex-1 p-6">
      <h1 class="text-2xl font-bold mb-6">Lịch Sử Mượn Sách</h1>
      <DataTable
        :rows="books"
        :columns="columns"
        :sortable="true"
        :filterable="true"
        :pagination="true"
        :rowsPerPage="5"
      />
    </main>
  </div>
</template>

<script>
import Sidebar from "@/components/commons/SideBar.vue";
import DataTable from "@/components/commons/DataTable.vue";

export default {
  name: "HomeView",
  components: {
    Sidebar,
    DataTable,
  },
  data() {
    return {
      books: [
        {
          id: 1,
          name: "Book 1",
          author: "Author 1",
          price: 100000,
          quantity: 5,
          borrowDate: "2024-11-01",
        },
        {
          id: 1,
          name: "Book 1",
          author: "Author 1",
          price: 100000,
          quantity: 5,
          borrowDate: "2024-11-01",
        },
        {
          id: 1,
          name: "Book 1",
          author: "Author 1",
          price: 100000,
          quantity: 5,
          borrowDate: "2024-11-01",
        },
        {
          id: 1,
          name: "Book 1",
          author: "Author 1",
          price: 100000,
          quantity: 5,
          borrowDate: "2024-11-01",
        },
        {
          id: 1,
          name: "Book 1",
          author: "Author 1",
          price: 100000,
          quantity: 5,
          borrowDate: "2024-11-01",
        },
        {
          id: 1,
          name: "Book 1",
          author: "Author 1",
          price: 100000,
          quantity: 5,
          borrowDate: "2024-11-01",
        },
        {
          id: 1,
          name: "Book 1",
          author: "Author 1",
          price: 100000,
          quantity: 5,
          borrowDate: "2024-11-01",
        },
      ],
      columns: [
        { field: "id", header: "ID", sortable: true },
        { field: "name", header: "Tên Sách", sortable: true, filter: true },
        { field: "author", header: "Tác Giả", sortable: true, filter: true },
        { field: "price", header: "Đơn Giá", sortable: true },
        { field: "quantity", header: "Số Lượng", filter: true },
        { field: "borrowDate", header: "Ngày mượn", sortable: true },
      ],
    };
  },
};
</script>

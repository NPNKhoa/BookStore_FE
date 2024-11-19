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
          category: "Fiction",
          name: "Book 1",
          author: "Author 1",
          language: "English",
          quantity: 5,
          status: "Available",
          borrowDate: "2024-11-01",
          dueDate: "2024-11-30",
        },
        {
          id: 2,
          category: "Non-fiction",
          name: "Book 2",
          author: "Author 2",
          language: "Vietnamese",
          quantity: 2,
          status: "Borrowed",
          borrowDate: "2024-11-10",
          dueDate: "2024-12-01",
        },
        {
          id: 2,
          category: "Non-fiction",
          name: "Book 2",
          author: "Author 2",
          language: "Vietnamese",
          quantity: 2,
          status: "Borrowed",
          borrowDate: "2024-11-10",
          dueDate: "2024-12-01",
        },
        {
          id: 2,
          category: "Non-fiction",
          name: "Book 2",
          author: "Author 2",
          language: "Vietnamese",
          quantity: 2,
          status: "Borrowed",
          borrowDate: "2024-11-10",
          dueDate: "2024-12-01",
        },
        {
          id: 2,
          category: "Non-fiction",
          name: "Book 2",
          author: "Author 2",
          language: "Vietnamese",
          quantity: 2,
          status: "Borrowed",
          borrowDate: "2024-11-10",
          dueDate: "2024-12-01",
        },
        {
          id: 2,
          category: "Non-fiction",
          name: "Book 2",
          author: "Author 2",
          language: "Vietnamese",
          quantity: 2,
          status: "Borrowed",
          borrowDate: "2024-11-10",
          dueDate: "2024-12-01",
        },
        {
          id: 2,
          category: "Non-fiction",
          name: "Book 2",
          author: "Author 2",
          language: "Vietnamese",
          quantity: 2,
          status: "Borrowed",
          borrowDate: "2024-11-10",
          dueDate: "2024-12-01",
        },
      ],
      columns: [
        { field: "id", header: "ID", sortable: true },
        { field: "category", header: "Thể Loại", sortable: true, filter: true },
        { field: "name", header: "Tên Sách", sortable: true, filter: true },
        { field: "author", header: "Tác Giả", sortable: true },
        { field: "language", header: "Ngôn Ngữ", filter: true },
        { field: "quantity", header: "Số Lượng", sortable: true },
        { field: "status", header: "Trạng Thái" },
        { field: "borrowDate", header: "Ngày Mượn", sortable: true },
        { field: "dueDate", header: "Ngày Hết Hạn", sortable: true },
      ],
    };
  },
};
</script>

<template>
  <div class="flex h-screen">
    <SideBar />

    <main
      class="flex flex-col gap-16 p-6 h-full overflow-auto no-scrollbar w-[80%]"
    >
      <div class="flex justify-between items-start h-full">
        <div class="bg-white p-6 rounded shadow-lg shadow-slate-400 w-1/4">
          <h3 class="text-lg font-semibold">Số sách đang được mượn</h3>
          <div class="flex items-center justify-between mt-8">
            <span class="text-3xl font-bold">{{ borrowedBooks }}</span>
            <p class="text-gray-400">Trên tổng số {{ totalBooks }} quyển</p>
          </div>
        </div>

        <div
          class="bg-white p-4 rounded shadow-lg shadow-slate-400 w-[70%] h-[30rem]"
        >
          <h3 class="text-lg font-semibold mb-4">Thống kê sách</h3>
          <BarChartWrapper
            :chart-data="chartData"
            :chart-options="chartOptions"
          />
        </div>
      </div>

      <div class="flex justify-between items-center">
        <div class="bg-white p-4 rounded shadow-lg shadow-slate-400 w-[47%]">
          <h3 class="text-lg font-semibold mb-4">Top Độc Giả</h3>
          <DataTable
            :rows="topReaders"
            :columns="topReaderColumns"
            :sortable="true"
            :pagination="true"
          />
        </div>

        <div class="bg-white p-4 rounded shadow-lg shadow-slate-400 w-[47%]">
          <h3 class="text-lg font-semibold mb-4">Top Sách Yêu Thích</h3>
          <DataTable
            :rows="topBooks"
            :columns="topBooksColumns"
            :sortable="true"
            :pagination="true"
          />
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import BarChartWrapper from "@/components/statistic/BarChartWrapper.vue";
import DataTable from "@/components/commons/DataTable.vue";
import SideBar from "@/components/commons/SideBar.vue";

export default {
  name: "StatisticView",
  components: {
    BarChartWrapper,
    DataTable,
    SideBar,
  },
  data() {
    return {
      borrowedBooks: 10,
      totalBooks: 10,
      chartData: {
        labels: [
          "January",
          "February",
          "March",
          "April",
          "May",
          "June",
          "July",
          "August",
          "September",
          "October",
          "November",
          "December",
        ],
        datasets: [
          {
            label: "Số sách người đang mượn",
            backgroundColor: "#42A5F5",
            data: [5, 10, 15],
          },
          {
            label: "Tổng số sách hiện có",
            backgroundColor: "#FF6384",
            data: [10, 10, 10],
          },
        ],
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend: {
            position: "top",
          },
          title: {
            display: true,
            text: "Thống kê mượn sách",
          },
        },
        scales: {
          y: {
            beginAtZero: true,
          },
        },
      },
      topReaders: [
        { id: 1, name: "Nhà Xuất Bản Văn Học", borrowCount: 10 },
        { id: 1, name: "Nhà Xuất Bản Văn Học", borrowCount: 10 },
        { id: 1, name: "Nhà Xuất Bản Văn Học", borrowCount: 10 },
        { id: 1, name: "Nhà Xuất Bản Văn Học", borrowCount: 10 },
        { id: 1, name: "Nhà Xuất Bản Văn Học", borrowCount: 10 },
        { id: 1, name: "Nhà Xuất Bản Văn Học", borrowCount: 10 },
        { id: 1, name: "Nhà Xuất Bản Văn Học", borrowCount: 10 },
        { id: 1, name: "Nhà Xuất Bản Văn Học", borrowCount: 10 },
      ],
      topReaderColumns: [
        { field: "id", header: "ID" },
        { field: "name", header: "Tên Người Dùng" },
        { field: "borrowCount", header: "Số Lần Mượn Sách" },
      ],
      topBooks: [
        {
          id: 1,
          name: "Hai số phận (bìa cứng)",
          borrowCount: 20,
        },
        {
          id: 1,
          name: "Hai số phận (bìa cứng)",
          borrowCount: 20,
        },
        {
          id: 1,
          name: "Hai số phận (bìa cứng)",
          borrowCount: 20,
        },
        {
          id: 1,
          name: "Hai số phận (bìa cứng)",
          borrowCount: 20,
        },
        {
          id: 1,
          name: "Hai số phận (bìa cứng)",
          borrowCount: 20,
        },
        {
          id: 1,
          name: "Hai số phận (bìa cứng)",
          borrowCount: 20,
        },
        {
          id: 1,
          name: "Hai số phận (bìa cứng)",
          borrowCount: 20,
        },
        {
          id: 1,
          name: "Hai số phận (bìa cứng)",
          borrowCount: 20,
        },
      ],
      topBooksColumns: [
        { field: "name", header: "Tên Sách" },
        {
          field: "borrowCount",
          header: "Số Lần Được Mượn",
        },
      ],
    };
  },
};
</script>

<style scoped>
canvas#bar-chart {
  height: 100px !important;
}
</style>

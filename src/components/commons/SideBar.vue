<template>
  <aside
    class="bg-gray-800 text-white h-screen flex flex-col justify-between p-4 w-64"
  >
    <div
      class="text-2xl font-bold mb-4 w-full flex flex-col gap-6 justify-center items-center"
    >
      <div class="flex justify-between items-center">
        <img alt="Vue logo" src="@/assets/logo.svg" class="w-1/4" />
        <h1 class="text-base">Book Management</h1>
      </div>
      <hr class="bg-slate-600 block w-full" />
    </div>

    <nav class="flex-1">
      <ul class="space-y-4">
        <li
          v-for="item in menuItems"
          :key="item.label"
          :class="[
            'hover:bg-gray-700 rounded',
            { 'bg-gray-600': isActive(item.to) },
          ]"
        >
          <router-link :to="item.to" class="flex items-center gap-2 p-2">
            <i :class="item.icon"></i>
            <span>{{ item.label }}</span>
          </router-link>
        </li>
      </ul>
    </nav>

    <button
      @click="signOut"
      class="bg-red-500 hover:bg-red-600 text-white py-2 rounded text-center w-full flex justify-center gap-2 items-center"
    >
      Sign Out
      <i class="pi pi-sign-out"></i>
    </button>
  </aside>
</template>

<script>
export default {
  name: "SideBar",
  data() {
    return {
      menuItems: [
        { label: "Home", to: "/", icon: "pi pi-home" },
        { label: "Search", to: "/search", icon: "pi pi-search" },
        { label: "Books", to: "/books", icon: "pi pi-book" },
        { label: "Admin", to: "/admin", icon: "pi pi-cog" },
      ],
    };
  },
  methods: {
    signOut() {
      console.log("Sign Out");
    },
    isActive(route) {
      return this.$route.path === route;
    },
  },
};
</script>

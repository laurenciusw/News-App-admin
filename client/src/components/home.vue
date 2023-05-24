<template>
  <div>
    <main class="min-h-screen w-full bg-gray-100 text-gray-700" x-data="layout">
      <!-- header page -->
      <header
        class="flex w-full items-center justify-between border-b-2 border-gray-200 bg-white p-2"
      >
        <!-- logo -->
        <div class="flex items-center space-x-2">
          <button type="button" class="text-3xl" @click="asideOpen = !asideOpen">
            <i class="bx bx-menu"></i>
          </button>
          <div>Logo</div>
        </div>
        <div>
          <button
            type="button"
            @click="profileOpen = !profileOpen"
            class="h-9 w-9 overflow-hidden rounded-full"
          >
            <img src="https://plchldr.co/i/40x40?bg=111111" alt="plchldr.co" />
          </button>
        </div>
      </header>

      <div class="flex sticky top-0">
        <!-- aside -->
        <aside
          class="flex w-72 flex-col space-y-2 border-r-2 border-gray-200 bg-white p-2 sticky top-0"
          style="height: 90.5vh"
          :class="{ hidden: !asideOpen }"
        >
          <a
            @click.prevent="changeSection('dashboard')"
            class="flex items-center space-x-1 rounded-md px-2 py-3 hover:bg-gray-100 hover:text-blue-600"
          >
            <span class="text-2xl"><i class="bx bx-home"></i></span>
            <span>home</span>
          </a>
          <a
            @click.prevent="changeSection('article')"
            class="flex items-center space-x-1 rounded-md px-2 py-3 hover:bg-gray-100 hover:text-blue-600 cursor-pointer"
          >
            <span class="text-2xl"><i class="bx bx-food-menu"></i></span>
            <span>Articles</span>
          </a>
          <a
            @click.prevent="changeSection('category')"
            class="flex items-center space-x-1 rounded-md px-2 py-3 hover:bg-gray-100 hover:text-blue-600 cursor-pointer"
          >
            <span class="text-2xl"><i class="bx bx-category-alt"></i></span>
            <span>Category</span>
          </a>

          <a
            @click.prevent="changeSection('history')"
            class="flex items-center space-x-1 rounded-md px-2 py-3 hover:bg-gray-100 hover:text-blue-600 cursor-pointer"
          >
            <span class="text-2xl"><i class="bx bx-history"></i></span>
            <span>History</span>
          </a>

          <br />
          <br />

          <hr />

          <a
            @click.prevent="doLogout"
            class="flex items-center space-x-1 rounded-md px-2 py-3 hover:bg-gray-100 hover:text-blue-600 cursor-pointer"
          >
            <span class="text-2xl"><i class="bx bx-log-out"></i></span>
            <span>logout</span>
          </a>
        </aside>

        <!-- main content page -->
        <div class="container mx-auto px-4 sm:px-8">
          <div class="py-8">
            <!-- table -->
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      asideOpen: true,
      currentSection: ''
    }
  },
  components: {},
  methods: {
    changeSection(destination) {
      console.log(destination)
      this.currentSection = destination
    },
    doLogout() {
      this.$emit('handleLogout')
    }
  },
  created() {}
}
</script>

<style></style>

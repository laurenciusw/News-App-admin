<template>
  <div class="-mx-4 sm:-mx-8 px-4 sm:px-8 py-4 overflow-x-auto">
    <div class="my-2 flex sm:flex-row flex-col justify-end"></div>
    <div class="inline-block min-w-full shadow rounded-lg overflow-hidden">
      <table class="min-w-full leading-normal">
        <thead>
          <tr>
            <th
              v-for="(column, index) in columns"
              :key="index"
              class="px-6 py-5 border-b-2 border-gray-200 bg-gray-100 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider"
            >
              {{ column.label }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(data, index) in data" :key="index">
            <td
              class="px-5 py-5 border-b border-gray-200 bg-white text-sm w-10"
              v-for="(column, index) in columns"
              :key="index"
            >
              <div v-if="column.field == 'imgUrl'">
                <img :src="data.imgUrl" alt="error" class="w-full h-20" />
              </div>

              <div v-else-if="column.field == 'action'">
                <a
                  @click.prevent="detailArtcile(data.id)"
                  class="flex items-center hover:text-blue-600"
                >
                  <span class="text-2xl"><i class="bx bx-edit-alt"></i></span>
                </a>
              </div>

              <div v-else-if="column.field == 'status'">
                <select @change="updateStatus(data.id, $event.target.value)">
                  <option class="bg-white text-black" :selected="data.status == 'Active'">
                    Active
                  </option>
                  <option class="bg-white text-black" :selected="data.status == 'Inactive'">
                    Inactive
                  </option>
                  <option class="bg-white text-black">Archived</option>
                </select>
              </div>

              <div v-else>
                {{ data[column.field] }}
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
export default {
  props: ['columns', 'data'],
  methods: {
    detailArtcile(id) {
      console.log(id)
      this.$emit('detailArtcile', id)
    },
    updateStatus(id, status) {
      this.$emit('updateStatus', id, status)
    }
  },
  data() {
    return {
      newStatus: ''
    }
  }
}
</script>

<style></style>

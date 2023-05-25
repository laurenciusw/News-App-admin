<template>
  <reuseableTable :columns="columns" :data="categories" />
</template>

<script>
import reuseableTable from './reuseableTable.vue'

export default {
  components: {
    reuseableTable
  },
  props: ['categories'],
  data() {
    return {
      columns: [
        { label: 'no', field: 'id' },
        { label: 'nama', field: 'name' }
      ]
    }
  }
}
</script>

<style></style>

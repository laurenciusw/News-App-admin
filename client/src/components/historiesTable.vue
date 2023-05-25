<template>
  <reuseableTable :columns="columns" :data="formatedData" />
</template>

<script>
import reuseableTable from './reuseableTable.vue'

export default {
  components: {
    reuseableTable
  },
  props: ['histories'],
  data() {
    return {
      columns: [
        { label: 'no', field: 'id' },
        { label: 'title', field: 'title' },
        { label: 'descriptopn', field: 'description' },
        { label: 'updatedBy', field: 'updatedBy' },
        { label: 'createdAt', field: 'createdAt' }
      ]
    }
  },
  computed: {
    formatedData() {
      return this.histories.map((el, index) => {
        el.num = index + 1
        return el
      })
    }
  }
}
</script>

<style></style>

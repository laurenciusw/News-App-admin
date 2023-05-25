<template>
  <div>
    <reuseableTable
      :columns="columns"
      :data="formatedData"
      @detailArtcile="detailArtcile"
      @updateStatus="updateStatus"
    />
  </div>
</template>

<script>
import reuseableTable from './reuseableTable.vue'

export default {
  name: 'articlesTable',
  components: {
    reuseableTable
  },
  props: ['articles'],
  data() {
    return {
      columns: [
        { label: 'no', field: 'num' },
        { label: 'title', field: 'title' },
        { label: 'image', field: 'imgUrl' },
        { label: 'content', field: 'content' },
        { label: 'author', field: 'author' },
        { label: 'status', field: 'status' },
        { label: 'action', field: 'action' }
      ]
    }
  },
  computed: {
    formatedData() {
      return this.articles.map((el, index) => {
        el.num = index + 1
        el.author = el.User.email
        return el
      })
    }
  },
  methods: {
    detailArtcile(id) {
      this.$emit('detailArtcile', id)
    },
    updateStatus(id, status) {
      this.$emit('updateStatus', id, status)
    }
  }
}
</script>

<style></style>

<template>
  <a href="#" @click.prevent="handleClick" name="HeadSort" :class="clsTextStyle">
    <font-awesome-icon :icon="cls"></font-awesome-icon>
  </a>
</template>
<script>
/**
 * Sorting arrows within <th>
 */
export default {
  name: 'HeadSort',
  props: {
    field: { type: String, required: true },
    query: { type: Object, required: true }
  },
  data: () => ({
    order: ''
  }),
  computed: {
    cls () {
      const { order } = this
      if (!order) {
        return 'sort'
      } else if (order === 'asc') {
        return 'sort-up'
      } else if (order === 'desc') {
        return 'sort-down'
      }
    },
    clsTextStyle () {
      const { order } = this
      return !order ? 'text-muted': ''
    }
  },
  watch: {
    query: {
      handler ({ sort: field, order }) {
        this.order = field === this.field ? order : ''
      },
      deep: true,
      immediate: true
    }
  },
  methods: {
    handleClick () {
      const { query, order } = this
      query.sort = this.field
      query.order = this.order = order === 'desc' ? 'asc' : 'desc'
    }
  }
}
</script>

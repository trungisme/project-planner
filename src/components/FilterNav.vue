<template>
  <nav class="filter-nav">
    <button 
      v-for="(filter, index) in filters"
      :key="index"
      @click="updateFilter(filter)"
      :class="{ active: filter === current }">
      View {{filter}}
    </button>
  </nav>
</template>

<script>
export default {
  props: ['current'],
  data: () => ({
    filters: [ 'all', 'completed', 'ongoing']
  }),
  methods: {
    updateFilter(by) {
      this.$emit('filterChange', by)
    }
  }
}
</script>

<style>
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  outline: none;
  font-size: 12px;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button.active {
  color: #555;
}
</style>
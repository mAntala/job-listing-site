<template>
    <section v-if="filters.length > 0" class="filters">
        <filters-item :filters="filters" @clear-filter="clearFilter" />
        <filters-clear @clear-all="clearAllFilters" />
    </section>
</template>

<script>
import FiltersItem from '@/components/FiltersItem'
import FiltersClear from '@/components/FiltersClear'

export default {
    name: 'filters',
    components: {
        FiltersItem,
        FiltersClear
    },
    data() {
        return {
            filters: ['Frontend']
        }
    },
    methods: {
        clearAllFilters() {
            this.filters = []
        },
        clearFilter(filter) {
            let index = this.filters.indexOf(filter);
            this.filters.splice(index, 1);
        }
    }
}
</script>

<style lang="scss" scoped>
.filters {
    padding: 1rem 2rem;
    background-color: rgb(255, 255, 255);
    border-radius: 0.25rem;
    display: flex;
    justify-content: space-between;
    box-shadow: 0 6px 10px rgba(0, 0, 0, 0.15);
}
</style>
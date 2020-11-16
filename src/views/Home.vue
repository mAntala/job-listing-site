<template>
    <section class="home">
        <filters :activeFilters="filters" @remove-filter="removeFilter($event)" @remove-all-filters="removeAllFilters" />
        <jobs @select-filter="selectFilter($event)" :activeFilters="filters" />
    </section>
</template>

<script>
import Filters from '@/components/Filters'
import Jobs from '@/components/Jobs'

export default {
    name: 'Home',
    components: {
        Filters,
        Jobs
    },
    data() {
        return {
            filters: []
        }
    },
    methods: {
        selectFilter(filterName) {
            if(this.filters.includes(filterName)) {
                return
            }

            this.filters.push(filterName)
        },
        removeFilter(filterName) {
            let index = this.filters.indexOf(filterName)
            this.filters.splice(index, 1)
        },
        removeAllFilters() {
            this.filters.length = 0
        }
    }
}
</script>

<style lang="scss" scoped>
.home {
    max-width: 1100px;
    margin: 0 auto;
}
</style>
<template>
    <section :class="{ 'filters--hidden': filters.length === 0 }" class="filters">
        <section class="filters__container">
            <filters-item v-for="(filter, index) in filters" :key="index" :filterName="filter" @remove-filter="removeFilter($event)" />
        </section>
        <filters-remove-all @remove-all-filters="removeAllFilters" />
    </section>
</template>

<script>
import { ref } from 'vue'
import FiltersItem from '@/components/FiltersItem'
import FiltersRemoveAll from '@/components/FiltersRemoveAll'

export default {
    name: 'filters',
    emits: ['remove-filter', 'remove-all-filters'],
    components: {
        FiltersItem,
        FiltersRemoveAll
    },
    props: {
        activeFilters: {
            type: Array,
            default: () => {
                return []
            }
        }
    },
    setup(props) {
        const filters = ref(props.activeFilters)

        return {
            filters
        }
    },
    methods: {
        removeFilter(filterName) {
            this.$emit('remove-filter', filterName)
        },
        removeAllFilters() {
            this.$emit('remove-all-filters')
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
    margin: 0 0 2rem;
    transition: all .15s ease-in-out;

    &--hidden {
        opacity: 0;
        visibility: hidden;
        position: absolute;
        top: 2rem;
        left: 0;
        right: 0;
        margin: auto;
    }

    @media screen and (max-width: 767px) {
        width: calc(100% - 6rem);
        margin: 0 auto 3rem auto;
    }

    &__container {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: flex-start;
        width: 100%;
    }
}
</style>
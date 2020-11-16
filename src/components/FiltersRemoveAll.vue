<template>
    <button class="filters-clear" @click="removeAllFilters">
        Clear
    </button>
</template>

<script>
export default {
    name: 'filters-remove-all',
    emits: ['remove-all-filters'],
    methods: {
        removeAllFilters() {
            this.$emit('remove-all-filters')
        }
    }
}
</script>

<style lang="scss" scoped>
.filters-clear {
    background-color: transparent;
    color: rgb(105, 158, 156);

    &:hover {
        text-decoration: underline;
    }
}
</style>
<template>
    <button class="filters-clear" @click="clearAllFilters">
        Clear
    </button>
</template>

<script>
export default {
    name: 'filters-clear',
    emits: ['clear-all'],
    methods: {
        clearAllFilters() {
            this.$emit('clear-all');
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
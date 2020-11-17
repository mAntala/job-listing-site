<template>
    <span class="filter-item">
        <span class="filter-item__content">
            {{ filterName }}
        </span>

        <button class="filter-item__close" @click="removeFilter(filterName)">
            <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="times" class="svg-inline--fa fa-times fa-w-11" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 352 512"><path d="M242.72 256l100.07-100.07c12.28-12.28 12.28-32.19 0-44.48l-22.24-22.24c-12.28-12.28-32.19-12.28-44.48 0L176 189.28 75.93 89.21c-12.28-12.28-32.19-12.28-44.48 0L9.21 111.45c-12.28 12.28-12.28 32.19 0 44.48L109.28 256 9.21 356.07c-12.28 12.28-12.28 32.19 0 44.48l22.24 22.24c12.28 12.28 32.2 12.28 44.48 0L176 322.72l100.07 100.07c12.28 12.28 32.2 12.28 44.48 0l22.24-22.24c12.28-12.28 12.28-32.19 0-44.48L242.72 256z"></path></svg>
        </button>
    </span>
</template>

<script>
export default {
    name: 'filters-item',
    emits: ['remove-filter'],
    props: {
        filterName: {
            type: String,
            required: true
        }
    },
    methods: {
        removeFilter(filterName) {
            this.$emit('remove-filter', filterName)
        }
    }
}
</script>

<style lang="scss" scoped>
.filter-item {
    position: relative;
    display: flex;
    align-items: center;
    margin-right: 0.5rem;

    @media screen and (max-width: 767px) {
        margin-bottom: 0.5rem;
    }

    &:last-of-type {
        margin-right: 0;

        @media screen and (max-width: 767px) {
            margin-bottom: 0;
        }
    }

    &__content {
        padding: 0.5rem;
        font-size: 0.75rem;
        background-color: rgb(239, 250, 250);
        color: rgb(105, 158, 156);
        border-top-left-radius: 0.25rem;
        border-bottom-left-radius: 0.25rem;
    }

    &__close {
        background-color: rgb(87, 166, 166);
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 0.25rem 0.5rem;
        border-top-right-radius: 0.25rem;
        border-bottom-right-radius: 0.25rem;
        transition: all .2s ease-in-out;

        &:hover {
            background-color: rgb(44, 58, 58);
        }

        & svg {
            width: 14px;
            fill: rgb(255, 255, 255);
        }
    }
}
</style>
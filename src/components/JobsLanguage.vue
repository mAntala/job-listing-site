<template>
    <span class="job-item__language" @click="selectFilter(language)">
        {{ language }}
    </span>
</template>

<script>
export default {
    name: 'jobs-language',
    emits: ['select-filter'],
    props: {
        language: {
            type: String,
            required: true
        }
    },
    methods: {
        selectFilter(filterName) {
            this.$emit('select-filter', filterName);
        }
    }
}
</script>

<style lang="scss" scoped>
.job-item__language {
    background-color:  hsl(180, 31%, 95%);
    color: #699e9c;
    font-size: 0.75rem;
    font-weight: 500;
    padding: 0.35rem 0.25rem;
    border-radius: 0.25rem;
    margin-right: 0.75rem;
    cursor: pointer;

    @media screen and (max-width: 767px) {
        margin-bottom: 0.75rem;
    }

    &:last-of-type {
        margin-right: 0;

        @media screen and (max-width: 767px) {
            margin-bottom: 0;
        }
    }
}
</style>
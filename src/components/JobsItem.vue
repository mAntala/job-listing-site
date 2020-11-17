<template>
    <article class="job-item" :class="{ 'job-item--featured': job.featured }" :id="'job-' + job.id">
        <header class="job-item__logo">
            <img :src="companyLogo" />
        </header>

        <main class="job-item__content">
            <header class="job-item__company">
                <span class="job-item__company-name">{{ job.company }}</span>
                <span v-if="job.new" class="job-item__new job-item__pill">New!</span>
                <span v-if="job.featured" class="job-item__featured job-item__pill">Featured</span>
            </header>

            <main class="job-item__position">
                <p>{{ job.position }}</p>
            </main>

            <footer class="job-item__meta">
                <span class="job-item__meta-info">{{ job.postedAt }}</span>
                <span class="job-item__meta-info">{{ job.contract }}</span>
                <span class="job-item__meta-info">{{ job.location }}</span>
            </footer>
        </main>

        <footer class="job-item__languages">
            <jobs-language :language="job.role" @select-filter="selectFilter($event)" />
            <jobs-language :language="job.level" @select-filter="selectFilter($event)" />
            <jobs-language v-for="(tool, index) in job.tools" :key="index" :language="tool" @select-filter="selectFilter($event)" />
            <jobs-language v-for="(language, index) in job.languages" :key="index" :language="language" @select-filter="selectFilter($event)" />
        </footer>
    </article>
</template>

<script>
import { ref, onMounted } from 'vue'
import JobsLanguage from '@/components/JobsLanguage'

export default {
    name: 'jobs-item',
    emits: ['select-filter'],
    components: {
        JobsLanguage
    },
    props: {
        job: {
            type: Object,
            required: true
        }
    },
    setup(props) {
        let companyLogo = ref([])

        onMounted(() => companyLogo.value = require(`@/assets/logo/${props.job.logo}`))

        return {
            companyLogo
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
.job-item {
    padding: 1.5rem 2rem;
    border-radius: 0.25rem;
    box-shadow: 0 6px 10px rgba(0, 0, 0, 0.15);
    margin-bottom: 1.25rem;
    display: flex;
    align-items: center;
    position: relative;
    background-color: #FFF;

    &--featured {
        &:before {
            content: '';
            width: 5px;
            height: 100%;
            position: absolute;
            left: 0;
            top: 0;
            background-color: rgb(90, 164, 163);
            border-top-left-radius: 0.25rem;
            border-bottom-left-radius: 0.25rem;
        }
    }

    &:last-of-type {
        margin-bottom: 0;
    }

    &__logo {
        margin-right: 1.5rem;
        width: 88px;
    }

    &__content {}

    &__company {}

    &__company-name {
        font-size: 0.75rem;
        color: #57a6a6;
        margin-right: 0.5rem;
    }

    &__featured {
        background-color: #2c3a3a;
    }

    &__new {
        background-color: #57a6a6;
    }

    &__meta {
        display: flex;
        align-items: center;
    }

    &__position {
        font-weight: 700;
        color: hsl(180, 14%, 20%);
        cursor: pointer;
        transition: all .2s ease-in-out;

        &:hover {
            color: #57a6a6;
        }
    }

    &__pill {
        padding: 0.35rem 0.4rem 0.25rem;
        border-radius: 10px;
        font-size: 0.65rem;
        text-transform: uppercase;
        color: #FFF;
        margin: 0;
        line-height: 1;
        display: inline-flex;
        align-items: center;
        flex: 0 0 auto;
        margin-right: 0.5rem;
        font-weight: 700;

        &:last-of-type {
            margin-right: 0;
        }
    }

    &__meta-info {
        font-size: 0.75rem;
        color: hsl(180, 8%, 52%);
        position: relative;
        margin-right: 2rem;
        display: inline;

        &::after {
            content: '';
            display: list-item;
            list-style-type: disc;
            position: absolute;
            right: -1.65rem;
            top: -0.05rem;
            bottom: 0;
            margin: auto 0;
        }

        &:last-of-type {
            &::after {
                display: none;
            }
        }
    }

    &__languages {
        display: flex;
        justify-content: flex-end;
        flex: 1 0 auto;
    }
}
</style>
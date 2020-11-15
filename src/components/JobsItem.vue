<template>
    <article class="job-item" :class="{ 'job-item--featured': job.featured }" :id="'job-' + job.id">
        <header class="job-item__logo">
            <img :src="companyLogo" />
        </header>

        <main class="job-item__content">
            <header class="job-item__company">
                <span class="job-item__company-name">{{ job.company }}</span>
                <span v-if="job.new" class="job-item__new">New!</span>
                <span v-if="job.featured" class="job-item__featured">Featured</span>
            </header>

            <main class="job-item__position">
                {{ job.position }}
            </main>

            <footer class="job-item__meta">
                <span class="job-item__meta-info">{{ job.postedAt }}</span>
                <span class="job-item__meta-info">{{ job.contract }}</span>
                <span class="job-item__meta-info">{{ job.location }}</span>
            </footer>
        </main>

        <footer class="job-item__tags">
        </footer>
    </article>
</template>

<script>
import { ref, onMounted } from 'vue'

export default {
    name: 'jobs-item',
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
    }

    &__company {}

    &__company-name {}

    &__featured {}

    &__new {}
}
</style>
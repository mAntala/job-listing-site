<template>
    <section class="jobs">
        <jobs-item v-for="job in dbJobs" :key="job.id" :job="job" @select-filter="selectFilter($event)" />
    </section>
</template>

<script>
import { ref, onMounted } from 'vue'
import JobsItem from '@/components/JobsItem'

export default {
    name: 'jobs',
    emits: ['select-filter'],
    components: {
        JobsItem
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
        const dbJobs = ref([])
        const filters = ref(props.activeFilters);

        const jobsRequest = async () => {
            const req = await fetch('http://localhost:3000/jobs')
                .then(data => data.json())
            dbJobs.value = await req
        }

        onMounted(jobsRequest)

        return {
            dbJobs,
            filters,
            jobsRequest
        }
    },
    methods: {
        selectFilter(filterName) {
            this.$emit('select-filter', filterName)
        }
    }
}
</script>
<template>
    <section class="jobs">
        <jobs-item v-for="job in filteredJobs" :key="job.id" :job="job" @select-filter="selectFilter($event)" />
    </section>
</template>

<script>
import { ref, reactive, onMounted, computed } from 'vue'
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
        const filters = reactive(props.activeFilters)
        const jobs = ref([])

        const jobsRequest = async () => {
            const req = await fetch('http://localhost:3000/jobs')
                .then(data => data.json())
            jobs.value = await req
        }

        const filteredJobs = computed(() => {
            // If there is no filter selected, return all jobs
            if(filters.length === 0) { return jobs.value }

            return jobs.value.filter(job => {
                return filters.some(filter => job.languages.includes(filter) || job.role === filter || job.level === filter || job.tools.includes(filter))
            })
        });

        onMounted(jobsRequest)

        return {
            jobs,
            filters,
            jobsRequest,
            filteredJobs
        }
    },
    methods: {
        selectFilter(filterName) {
            this.$emit('select-filter', filterName)
        }
    }
}
</script>
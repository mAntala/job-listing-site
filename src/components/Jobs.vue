<template>
    <section class="jobs">
        <jobs-item v-for="job in dbJobs" :key="job.id" :job="job" />
    </section>
</template>

<script>
import { ref, onMounted } from 'vue'
import JobsItem from '@/components/JobsItem'

export default {
    name: 'jobs',
    components: {
        JobsItem
    },
    setup() {
        const dbJobs = ref([])
        const jobsRequest = async () => {
            const req = await fetch('http://localhost:3000/jobs')
                .then(data => data.json())
            dbJobs.value = await req
        }

        onMounted(jobsRequest)

        return {
            dbJobs,
            jobsRequest
        }
    }
}
</script>
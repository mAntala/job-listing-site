<template>
    <section class="home">
        <filters />
        <jobs />
    </section>
</template>

<script>
import Filters from '@/components/Filters'
import Jobs from '@/components/Jobs'

export default {
    name: 'Home',
    components: {
        Filters,
        Jobs
    }
}
</script>

<style lang="scss" scoped>
.home {
    max-width: 1100px;
    margin: 0 auto;
}
</style>
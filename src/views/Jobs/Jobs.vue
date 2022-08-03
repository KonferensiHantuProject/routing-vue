<template>
    <h1>Pekerjaan</h1>

    <!-- Kalau lengthnya ada -->
    <div v-if="jobs.length">  
        <div v-for="job in jobs" :key="job.id" class="job">
            <router-link :to="{ name: 'JobDetail', params: { id: job.id } }">
                <h2>{{ job.title }}</h2>
            </router-link>
        </div>
    </div>

    <!-- Kalau array kosong -->
    <div v-else>
        <p>Loading Pekerjaan ...</p>
    </div>
</template>

<script>
export default {
    data(){
        return {
            jobs: []
        }
    },
    mounted() {
        // Fetching data and return promise
        fetch('http://localhost:3000/jobs')
            .then(res => res.json())
            .then(data => this.jobs = data)
            .catch(err => console.log(err.message))
    }
}
</script>

<style>
    .job h2{
        background: #f4f4f4;
        padding: 20px;
        border-radius: 10px;
        margin: 10px auto;
        max-width: 600px;
        cursor: pointer;
        color: #444;
    }
    .job h2:hover{
        background: #ddd;
    }
    .job a{
        text-decoration: none;
    }
</style>
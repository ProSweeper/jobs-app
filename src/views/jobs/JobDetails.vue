<template>
  <div v-if="job">
    <h1>{{ job.title }}</h1>
    <p>{{ job.details }}</p>
  </div>
  <div v-else>
    loading job details
  </div>
</template>

<script>
  export default {
    props: ['id',],
    data() {
      return {
        jobEndpoint: `http://localhost:3000/jobs/${this.id}`,
        job: null,
      }
    },
    mounted() {
      fetch(`${this.jobEndpoint}`)
        .then(res => res.json())
          .then(data => this.job = data)
          .catch(err => console.log(err.message))
    },
  }
</script>
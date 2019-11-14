<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Details of ' + this.event.title
        }
      ]
    }
  },
  async asyncData({ $axios, error, params }) {
    try {
      const { data } = await $axios.get(
        'http://localhost:8000/events/' + params.id
      )

      return {
        event: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch event detail at this time. Please try again'
      })
    }
  }
}
</script>

<style></style>

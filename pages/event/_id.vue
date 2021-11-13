<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
import EventService from "@/services/EventService";

export default {
  name: "event",
  head() {
    return {
      title: 'Event #' + this.id,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'What you need to know about Event #' + this.id
        }
      ]
    }
  },
  computed: {
    id() {
      return this.$route.params.id
    }
  },
  async asyncData(ctx) {
    const response = await EventService.getEvent(ctx.params.id);
    const event = response.data;
    return {event}
  }
}
</script>

<style scoped>

</style>

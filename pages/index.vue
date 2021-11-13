<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from "@/components/EventCard";

export default {
  head() {
    return {
      title: 'Event Listing'
    }
  },
  async fetch(ctx) {
    try {
      await ctx.store.dispatch('events/fetchEvents');
    } catch (e){
      ctx.error({ statusCode: 503, message: 'Unable to fetch events at this time, please try again' })
    }
  },
  components: {
    EventCard
  },
  computed: {
    events() {
      return this.$store.state.events.events
    }
  }
}
</script>

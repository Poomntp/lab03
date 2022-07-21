<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
  <div class="categories">
    <Categories v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script>
// @ is an alias to /src
import EventCard from "@/components/EventCard.vue";
import Categories from "@/components/Categories.vue";
import EventService from "@/services/EventService.js";
//axios from "axios";

export default {
  name: "EventListView",
  components: {
    EventCard, // register it as a child component
    Categories,
  },
  data() {
    return {
      events: null,
    };
  },
  created() {
    EventService.getEvents()
      .then((response) => {
        this.events = response.data;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>
<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.categories {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: right;
}
</style>

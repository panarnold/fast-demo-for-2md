<template>
  <div class="date-and-clock">
    <div class="">{{ formatedDate }}</div>
    <div>
      {{ formattedHour }}
    </div>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, ref } from "vue";
import { format } from "date-fns";

export default defineComponent({
  name: "DateAndClock",
  props: {},
  setup() {
    const formatedDate = ref(format(new Date(), "yyyy-MM-d"));
    const formattedHour = ref(format(new Date(), "HH:mm"));

    setInterval(() => {
      formatedDate.value = format(new Date(), "yyyy-MM-d");
      formattedHour.value = format(new Date(), "HH:mm");
    }, 1000);
    return {
      formatedDate,
      formattedHour,
    };
  },
});
</script>

<style scoped lang="scss">
.date-and-clock {
}
</style>

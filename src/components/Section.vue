<template>
  <div class="section">
    <div class="header">
      {{ header }}
    </div>
    <div class="content">
      <slot>
        {{ content }}
      </slot>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "section",
  props: {
    header: {
      type: String,
      required: true,
    },
    content: {
      type: String,
    },
  },
  setup() {
    return {};
  },
});
</script>

<style scoped lang="scss">
.section {
  display: grid;
  grid-auto-flow: row;
  row-gap: 1rem;
  .header {
    font-weight: bold;
  }
  .content {
    font-size: 0.8rem;
  }
}
</style>

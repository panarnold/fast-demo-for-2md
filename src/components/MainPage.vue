<template>
  <div class="main-page">
    <div class="main-content">
      <MainContent />
    </div>
    <div class="custom-footer">
      <CustomFooter />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import MainContent from "@/components/MainContent.vue";
import CustomFooter from "@/components/CustomFooter.vue";

export default defineComponent({
  name: "main-page",
  props: {},
  components: {
    MainContent,
    CustomFooter,
  },
  setup() {
    return {};
  },
});
</script>

<style scoped lang="scss">
.main-page {
  display: grid;
  grid-template-rows: 65vh 25vh;
  overflow-y: hidden;
}
</style>

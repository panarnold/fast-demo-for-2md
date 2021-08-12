<template>
  <div class="custom-footer">
    <div class="sections">
      <Section
        header="ABOUT YOU"
        content="HELLO. MY NAME IS ARNOLD AND I HAVE A STRONG WILLINGNESS TO WORK FOR YOU"
      ></Section>
      <Section header="DATE AND TIME">
        <DateAndClock />
      </Section>
      <Section header="CONTACT" content="cytrowskiarnold@gmail.com"></Section>
    </div>
    <div class="media-menu">
      <div v-for="icon in icons" :key="icon" class="icon">
        <a
          href="https://www.youtube.com/watch?v=8bvV2kqOFW4&t=38s"
          target="_blank"
        >
          <img :src="getIconUrl(icon)" alt="" />
        </a>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Section from "@/components/Section.vue";
import DateAndClock from "@/components/DateAndClock.vue";
import { icons } from "@/mixins/items";

export default defineComponent({
  name: "CustomFooter",
  props: {},
  components: {
    Section,
    DateAndClock,
  },

  setup() {
    function getIconUrl(iconUrl: string) {
      return require("../assets/" + iconUrl);
    }
    return {
      icons,
      getIconUrl,
    };
  },
});
</script>

<style scoped lang="scss">
.custom-footer {
  padding-top: 5rem;
  padding-bottom: 2rem;
  background: #2699fb;
  color: white;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-template-areas: "sections sections sections . . media";
  .sections {
    display: grid;
    grid-template-columns: repeat(3, 15rem);
    grid-area: sections;
  }
  .media-menu {
    grid-area: media;
    display: grid;
    grid-auto-flow: column;
    align-items: flex-start;
    justify-content: flex-end;
    .icon {
      height: 10px;
      img {
        width: 30%;
        filter: invert(100%);
      }
    }
  }
}
</style>

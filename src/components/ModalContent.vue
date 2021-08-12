<template>
  <div class="body">
    <div class="header">
      <div class="wrapper">
        <div class="name">GALLERY IN MODAL</div>
        <div class="x" @click="close()">X</div>
      </div>
      <div class="source"></div>
    </div>
    <div
      class="content"
      :style="{
        'background-image': `url(${content[currentIndex].source})`,
      }"
    >
      <div class="navigation">
        <button class="left-arrow" @click="changeItem('previous')">
          <svg
            version="1.1"
            id="Capa_1"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            x="0px"
            y="0px"
            viewBox="0 0 490 490"
            style="enable-background: new 0 0 490 490"
            xml:space="preserve"
          >
            <path
              d="M413.476,398.302L258.215,245L413.476,91.69L324.619,0L76.524,245l248.094,245L413.476,398.302z M120.086,245L324.14,43.502
	l46.252,47.71L214.653,245l155.739,153.781l-46.252,47.717L120.086,245z"
            />
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
          </svg>
        </button>
        <div class="image">
          <!-- {{ content[currentIndex].source }} -->
        </div>
        <button class="right-arrow" @click="changeItem('next')">
          <svg
            version="1.1"
            id="Capa_1"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            x="0px"
            y="0px"
            viewBox="0 0 490 490"
            style="enable-background: new 0 0 490 490"
            xml:space="preserve"
          >
            <path
              d="M413.476,398.302L258.215,245L413.476,91.69L324.619,0L76.524,245l248.094,245L413.476,398.302z M120.086,245L324.14,43.502
	l46.252,47.71L214.653,245l155.739,153.781l-46.252,47.717L120.086,245z"
            />
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
            <g></g>
          </svg>
        </button>
      </div>
      <div class="footer-element">
        <div class="author-name">
          {{ content[currentIndex].author }}
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import { ImageObject } from "@/mixins/items";

export default defineComponent({
  name: "ModalContent",
  props: {
    content: {
      type: Array as () => Array<ImageObject>,
      required: true,
    },
  },
  emits: ["close"],
  setup(props, { emit }) {
    function close() {
      emit("close", []);
    }

    const selectedImage = ref<ImageObject>(props.content[4]);
    const currentIndex = ref<number>(0);
    const images = ref<Array<ImageObject>>(props.content);

    // const selectedIndex = computed(() => {
    //   return indexOf(props.content, selectedImage.value);
    // });

    function changeItem(direction: string) {
      switch (direction) {
        case "previous":
          if (currentIndex.value === 0) {
            currentIndex.value = props.content.length - 1;
            console.log(currentIndex.value);
          } else currentIndex.value -= 1;

          break;
        case "next":
          if (currentIndex.value === props.content.length - 1) {
            currentIndex.value = 0;
          } else currentIndex.value += 1;

          break;
      }
    }

    return {
      close,
      selectedImage,
      changeItem,
      currentIndex,
      images,
    };
  },
});
</script>

<style scoped lang="scss">
button {
  height: 2rem;
  width: 2rem;
}
.body {
  .header {
    grid-area: header;
    background: #7fc4fd;
    height: 6rem;
    color: white;

    .wrapper {
      display: grid;
      grid-auto-flow: column;
      justify-content: space-between;
      height: inherit;
      align-items: center;
      padding-left: 2rem;
      padding-right: 2rem;
      .name {
        font-size: 0.8rem;
        font-weight: bolder;
      }
      .x {
        cursor: pointer;
        font-weight: bold;
      }
    }
  }
  .content {
    grid-area: content;
    display: grid;
    grid-auto-flow: row;
    justify-items: center;
    height: 20rem;
    width: 40rem;
    align-items: flex-end;
    background-size: cover;
    .navigation {
      display: grid;
      width: 35rem;
      grid-auto-flow: column;
      justify-content: space-between;
      // padding-left: 2rem;
      // padding-right: 2rem;

      .left-arrow {
        cursor: pointer;

        svg {
          transform: translateY(10%);
        }
      }
      .right-arrow {
        cursor: pointer;
        transform: rotate(180deg);
        svg {
          transform: translateY(10%);
        }
        // transform: translateY(10%);
      }
    }
    // padding-left: 2rem;
    // padding-right: 2rem;
    // // .image {
    //   width: 20rem;
    // }
    .footer-element {
      display: grid;
      width: inherit;
      grid-template-areas: "author .";

      .author-name {
        grid-area: author;
        background: #f0f9ff;
        border: 4px solid #bce0fd;
        border-radius: 4px;
        color: #2699fb;
        font-weight: bolder;
        font-size: 0.8rem;
        transform: translateY(-20%) translateX(4%);
        width: 15rem;
      }
    }
  }
}
</style>

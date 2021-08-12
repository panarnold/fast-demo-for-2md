<template>
  <div class="main-content">
    <div class="darker-place" :class="{ clicked: clicked }">
      <svg
        xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:cc="http://web.resource.org/cc/"
        xmlns:dc="http://purl.org/dc/elements/1.1/"
        xmlns:svg="http://www.w3.org/2000/svg"
        xmlns:inkscape="http://www.inkscape.org/namespaces/inkscape"
        xmlns:sodipodi="http://sodipodi.sourceforge.net/DTD/sodipodi-0.dtd"
        xmlns:ns1="http://sozi.baierouge.fr"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        id="svg2"
        viewBox="0 0 360 360"
        version="1.0"
        inkscape:version="0.91 r13725"
      >
        <g id="layer1">
          <path
            id="path3346"
            style="fill-rule: evenodd; fill: #bce0fd"
            d="m6.9767 178.6l86.602-150 86.601 150h-173.2z"
          />
          <path
            id="path3348"
            style="fill-rule: evenodd; fill: #bce0fd"
            d="m93.579 328.6l86.601-150 86.6 150h-173.2z"
          />
          <path
            id="path3350"
            style="fill-rule: evenodd; fill: #2699fb"
            d="m180.18 178.6l86.6-150 86.61 150h-173.21z"
          />
          <path
            id="path3352"
            style="fill-rule: evenodd; fill: #2699fb"
            d="m6.9767 178.6l86.602 150 86.601-150h-173.2z"
          />
          <path
            id="path3354"
            style="fill-rule: evenodd; fill: #bce0fd"
            d="m93.579 28.605l86.601 150 86.6-150-173.2 0.005z"
          />
          <path
            id="path3356"
            style="fill-rule: evenodd; fill: #bce0fd"
            d="m180.18 178.6l86.6 150 86.61-150h-173.21z"
          />
        </g>
        <metadata>
          <rdf:RDF>
            <cc:Work>
              <dc:format>image/svg+xml</dc:format>
              <dc:type rdf:resource="http://purl.org/dc/dcmitype/StillImage" />
              <cc:license
                rdf:resource="http://creativecommons.org/licenses/publicdomain/"
              />
              <dc:publisher>
                <cc:Agent rdf:about="http://openclipart.org/">
                  <dc:title>Openclipart</dc:title>
                </cc:Agent>
              </dc:publisher>
              <dc:title>hexagon 6 color</dc:title>
              <dc:date>2011-01-05T21:43:09</dc:date>
              <dc:description
                >The most colorful way to prove that a hexagon is six
                triangles!</dc:description
              >
              <dc:source
                >https://openclipart.org/detail/103795/hexagon-6-color-by-10binary</dc:source
              >
              <dc:creator>
                <cc:Agent>
                  <dc:title>10binary</dc:title>
                </cc:Agent>
              </dc:creator>
              <dc:subject>
                <rdf:Bag>
                  <rdf:li>color</rdf:li>
                  <rdf:li>hexagon</rdf:li>
                  <rdf:li>triangle</rdf:li>
                </rdf:Bag>
              </dc:subject>
            </cc:Work>
            <cc:License
              rdf:about="http://creativecommons.org/licenses/publicdomain/"
            >
              <cc:permits
                rdf:resource="http://creativecommons.org/ns#Reproduction"
              />
              <cc:permits
                rdf:resource="http://creativecommons.org/ns#Distribution"
              />
              <cc:permits
                rdf:resource="http://creativecommons.org/ns#DerivativeWorks"
              />
            </cc:License>
          </rdf:RDF>
        </metadata>
      </svg>
    </div>
    <div class="content" :class="{ clicked: clicked }">
      <h1>This is main page title</h1>
      <div class="main-text">
        Lorem ipsum dolor sit, amet consectetur adipisicing elit. Totam hic
        voluptatum cum vero eius ipsa iusto! Inventore aut eveniet eos nostrum,
        hic voluptatem ut ratione, eum sapiente architecto eaque nesciunt? Sequi
        magni rerum, reprehenderit iure commodi veritatis dolorum nemo
        architecto et non ratione corporis laudantium dolorem, officiis optio
        fuga suscipit assumenda numquam dicta odit debitis nisi! Molestias ad
        facere quae. Maxime veritatis nisi nulla quasi dolores quia voluptatem,
        ab distinctio minima, ea, quibusdam commodi aspernatur. Deleniti
        reiciendis, totam, exercitationem placeat unde harum, ex quod fugit
        cupiditate itaque repellendus nostrum similique? Reiciendis, quidem.
        Consequuntur placeat eius, dignissimos expedita ipsum quod? Sunt
        excepturi porro laudantium recusandae quia debitis praesentium quis
        libero, quas temporibus quaerat nesciunt, reiciendis illum dicta? Rerum
        sunt exercitationem possimus. Tempora est corrupti ipsam incidunt
        praesentium quidem cupiditate possimus? Nobis officiis dolorum sequi,
        eos optio enim iste, libero, perferendis obcaecati maiores a! Porro
        repellendus, laudantium suscipit necessitatibus laborum expedita hic?
      </div>
      <div class="buttons">
        <button class="more-button" @click="clicked = !clicked">MORE</button>
        <button class="gallery-button" @click="modalIsOpen = !modalIsOpen">
          SHOW GALLERY
        </button>
      </div>
    </div>
  </div>
  <Modal :visible="modalIsOpen">
    <ModalContent @close="modalIsOpen = false" :content="imageObjects" />
  </Modal>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from "vue";
import Modal from "@/components/Modal.vue";
import ModalContent from "@/components/ModalContent.vue";
import { ImageObject } from "@/mixins/items";
import { forEach } from "lodash";

export default defineComponent({
  name: "main-content",
  props: {},
  components: {
    Modal,
    ModalContent,
  },
  setup() {
    const clicked = ref<boolean>(false);
    const modalIsOpen = ref<boolean>(false);
    const imageObjects = ref<Array<ImageObject>>([]);

    function getImages(): Promise<number> {
      return new Promise((resolve) => {
        fetch("https://picsum.photos/v2/list?limit=10")
          .then((response) => response.json())
          .then((data) => {
            resolve(data);
            forEach(data, (item) => {
              imageObjects.value = [
                ...imageObjects.value,
                {
                  source: item.download_url,
                  author: item.author,
                },
              ];
            });
          });
      });
    }
    getImages();

    return {
      clicked,
      modalIsOpen,
      getImages,
      imageObjects,
    };
  },
});
</script>

<style scoped lang="scss">
button {
  border-radius: 4px;
  height: 3rem;
  width: 10rem;
  cursor: pointer;
}
.main-content {
  display: grid;
  grid-template-columns: repeat(10, 1fr);
  grid-template-areas: ". . . darker content content content . . .";
  height: 30vh;
  .darker-place {
    grid-area: darker;
    background: #7fc4fd;
    svg {
      transform: translateY(30%) translateX(-50%);
      transition: all 1s ease;
    }
    &.clicked {
      svg {
        transform: translateY(30%);
        transition: all 1s ease;
      }
    }
  }
  .content {
    display: grid;
    grid-template-rows: 5rem 2rem 4rem;
    padding-top: 2rem;
    row-gap: 2rem;
    grid-area: content;
    background: #f1f9ff;
    transition: all 1s ease;
    .main-text {
      padding-left: 1rem;
      padding-right: 1rem;
      display: inline-block;
      overflow: hidden;
      text-overflow: ellipsis;
      //   white-space: nowrap;
    }
    &.clicked {
      grid-template-rows: 5rem 20rem 4rem;

      transition: all 1s ease;
    }
    .buttons {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      grid-template-areas: ". more gallery . . .";
      grid-gap: 1rem;
      .more-button {
        grid-area: more;
        border: 1px #7fc4fd solid;
        background: none;
        color: #2699fb;
      }
      .gallery-button {
        grid-area: gallery;
        background: #2699fb;
        color: white;
        border: none;
      }
    }
  }
}
</style>

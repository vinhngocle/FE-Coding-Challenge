<template>
  <div class="mt-3">
    <div class="text-center mb-3">
      <b-button-group size="sm">
        <b-button>Save</b-button>
        <b-button>Undo</b-button>
        <b-button>Redo</b-button>
        <b-button>Export</b-button>
        <b-button>Import</b-button>
        <b-button @click="gotoConsumer">View</b-button>
      </b-button-group>
    </div>
    <div class="page-drag" @mousemove="mouseMove">
      <div class="page-left">
        <draggable
          id="drag-id-paragraph"
          @dragging="dragging"
          title="Paragraph"
        />
        <draggable
          id="drag-id-button"
          @dragging="dragging"
          title="Button"
          @textParagraph="textParagraph"
        />
      </div>
      <div class="page-right">
        <div class="row mt-3">
          <div class="col-md-6">
            <div>Mouse: ({{ clientX }}, {{ clientY }})</div>
            <div>Drapping: {{ dragStatus }}</div>
            <div>Instances: {{ instances }}</div>
            <div>
              Config:
              <span id="show-config"></span>
            </div>
          </div>
          <div class="col-md-6">
            <div id="demo"></div>
          </div>
        </div>
        <div class="col-md-12">
          <dropzone @draggingRemove="draggingRemove" @countDrops="countDrops" />
        </div>
        <div id="page-show-input">
          <div class="col-sm-3">
            <div id="demo-paragraph"></div>
          </div>
          <div class="col-sm-3">
            <div id="demo-input"></div>
          </div>
        </div>
      </div>
      <div class="page-clear"></div>
    </div>
  </div>
</template>

<script>
import Draggable from "../../components/Draggable.vue";
import Dropzone from "../../components/Dropzone.vue";
export default {
  name: "Admin",
  data() {
    return {
      clientX: 0,
      clientY: 0,
      instances: 0,
      config: {
        id: "id0.123123123",
        component: "ElementParagraph",
        props: {
          text: "",
          message: "",
        },
      },
      dragStatus: "",
      paragraphText: "",
      buttonText: "",
      message: "",
    };
  },
  components: {
    Draggable,
    Dropzone,
  },
  methods: {
    gotoConsumer() {
      let route = this.$router.resolve({ path: "/consumer" });
      window.open(route.href);
    },
    mouseMove(event) {
      this.clientX = event.clientX;
      this.clientY = event.clientY;
    },
    dragging(value) {
      this.dragStatus = value;
    },
    draggingRemove(value) {
      this.dragStatus = value;
    },
    countDrops(value) {
      this.instances = value;
    },
    textParagraph(value) {
      console.log('textParagraph', value);
      this.configs.props.text = value;
    }
  },
};
</script>

<style scoped>
.page-drag {
  border-top: 3px solid #aaa;
  margin-bottom: 10px;
}
.page-left {
  width: 200px;
  height: 700px;
  border-right: 3px solid #aaa;
  float: left;
}
.page-right {
  /* float: left; */
  margin-left: 200px;
  width: 90%;
  height: 400px;
  border-bottom: 3px solid #aaaaaa;
}
.page-clear {
  clear: both;
}
</style>

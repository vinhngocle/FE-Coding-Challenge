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
    <!-- <hr/> -->
    <!-- <draggable :id="paragraph" title="Paragraph"/> -->
    <!-- <draggable :id="button" title="Button"/> -->
    <div class="page-drag" @mousemove="mouseMove">
      <div class="page-left">
        <draggable @dragging="dragging" title="Paragraph" />
        <draggable @dragging="dragging" title="Button" />
      </div>
      <div class="page-right">
        <div class="row mt-3">
          <div class="col-md-6">
            <p>Mouse: ({{ clientX }}, {{ clientY }})</p>
            <p>Drapping: {{ drapStatus }}</p>
            <p>Instances: {{ instances }}</p>
            <p>Config:</p>
          </div>
          <div class="col-md-6">
            <b-button size="sm">button</b-button>
            <p>paragraph</p>
          </div>
        </div>
        <dropzone @draggingRemove="draggingRemove" @countDrops="countDrops" />
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
        props: {},
      },
      drapStatus: "",
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
      this.drapStatus = value;
      console.log("value", value);
    },
    draggingRemove(value) {
      this.drapStatus = value;
      console.log("draggingRemove", value);
    },
    countDrops(value) {
      this.instances = value;
    },
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

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
        <draggable id="drag-id-paragraph" @dragging="dragging" title="Paragraph" />
        <draggable id="drag-id-button" @dragging="dragging" title="Button" />
      </div>
      <div class="page-right">
        <div class="row mt-3">
          <div class="col-md-6">
            <p>Mouse: ({{ clientX }}, {{ clientY }})</p>
            <p>Drapping: {{ dragStatus }}</p>
            <p>Instances: {{ instances }}</p>
            <p>Config: {{ config }}</p>
          </div>
          <div class="col-md-6">
            <!-- <b-button size="sm">button</b-button>
            <p>paragraph</p> -->
            <div id="demo"></div>
          </div>
        </div>
        <div class="col-md-12">
          <dropzone @draggingRemove="draggingRemove" @countDrops="countDrops" />
        </div>
        <div id="page-show-input">
          <!-- <div class="col-sm-3">
            <p>Paragraph Text</p>
            <b-form-input v-model="paragraphText"></b-form-input>
          </div>
          <div class="col-sm-3">
            <p>Button Text</p>
            <b-form-input v-model="buttonText"></b-form-input>
          </div>
          <div class="col-sm-3">
            <p>Alert Message</p>
            <b-form-input v-model="message"></b-form-input>
          </div> -->
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
      console.log("value", value);
      // if (value === "ElementParagraph") {
      //   const node = document.createElement("div");
      //   const textnode = document.createTextNode("Paragraph");
      //   node.appendChild(textnode);
      //   document.getElementById("demo").appendChild(node)
      // } else {
      //   const node = document.createElement("button");
      //   const textnode = document.createTextNode("Button");
      //   node.appendChild(textnode);
      //   document.getElementById("demo").appendChild(node)
      // }
    },
    draggingRemove(value) {
      this.dragStatus = value;
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

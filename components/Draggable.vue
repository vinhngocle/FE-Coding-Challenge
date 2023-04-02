<template>
  <div class="mt-3">
    <div class="droptarget" @drop="handleDrop" @dragover="allowDrop">
      <p
        id="dragtarget"
        @dragstart="handleDragStart"
        @drag="handleDragging"
        draggable="true"
        @drop.prevent="handleDrop"
        @dragover.prevent
      >
        {{ title }}
      </p>
    </div>
    <!-- <p class="droptarget" @drop="handleDrop" @dragover="allowDrop"></p> -->
    <span id="demo"></span>
  </div>
</template>

<script>
export default {
  components: {},
  name: "Draggable",
  props: {
    title: {
      type: String,
      default: "",
    },
  },
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
    };
  },
  methods: {
    handleDragStart(event) {
      const target = event.target;
      event.dataTransfer.setData("Text", target.id);
      event.dataTransfer.dropEffect = 'move'
      event.dataTransfer.effectAllowed = 'move'
    },
    handleDragging(event) {
      if (this.title === "Button") {
        this.$emit("dragging", "ElementButton")
        console.log("button");
      } else {
        this.$emit("dragging", "ElementParagraph")
        console.log("Paragraph");
      }
      document.getElementById("demo").innerHTML =
        "The p element is being dragged";
    },
    allowDrop(event) {
      event.preventDefault();
    },
    handleDrop(event) {
      const target = event.target;
      event.preventDefault();
      const data = event.dataTransfer.getData("Text");
      target.appendChild(document.getElementById(data));
      event.dataTransfer.clearData();
      document.getElementById("demo").innerHTML = "The p element was dropped";
    },
  },
};
</script>

<style scoped>
#app {
  border-top: 3px solid #aaaaaa;
}
.droptarget {
  width: 100px;
  height: 35px;
  margin: 0 15px 15px 15px;
  padding: 10px;
  border: 1px solid #aaaaaa;
}
</style>

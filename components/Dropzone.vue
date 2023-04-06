<template>
  <div class="mt-3">
    <span id="demo"></span>
    <p class="droptarget" @drop="handleDrop" @dragover="allowDrop"></p>
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

      countDrops: 0,
    };
  },
  methods: {
    allowDrop(event) {
      event.preventDefault();
    },
    handleDrop(event) {
      event.preventDefault();
      const target = event.target;
      // const data = event.dataTransfer.getData("drag-id-paragraph")
      // console.log('data target.id drop', data);
      // target.appendChild(document.getElementById(data));


      // if (target.id === "drag-id-paragraph") {
        // const node = document.createElement("div");
        // const textnode = document.createTextNode("Paragraph");
        // node.appendChild(textnode);
        // document.getElementById("demo").appendChild(node)
      // } else {
      //   const node = document.createElement("button");
      //   const textnode = document.createTextNode("Button");
      //   node.appendChild(textnode);
      //   document.getElementById("demo").appendChild(node)
      // }

      const data = event.dataTransfer.getData("drag-id-paragraph");
      // target.appendChild(document.getElementById(data));


      // document.getElementById("demo").appendChild(node);

      event.dataTransfer.clearData();

      if (event.stopPropagation) event.stopPropagation();
      this.countDrops++;
      this.$emit("draggingRemove", "");
      this.$emit("countDrops", this.countDrops);
    },
  },
};
</script>

<style scoped>
#app {
  border-top: 3px solid #aaaaaa;
}
.droptarget {
  width: 100%;
  height: 200px;
  padding: 10px;
  border: 1px solid #aaaaaa;
}
</style>

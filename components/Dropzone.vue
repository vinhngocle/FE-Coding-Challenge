<template>
  <div class="mt-3">
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
      event.dataTransfer.clearData();

      if (event.stopPropagation) event.stopPropagation();
      this.countDrops++;
      this.$emit("draggingRemove", "");
      this.$emit("countDrops", this.countDrops);

      console.log("event drop", event);
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
  height: 237px;
  margin: 0 15px 15px 15px;
  padding: 10px;
  border: 1px solid #aaaaaa;
}
</style>

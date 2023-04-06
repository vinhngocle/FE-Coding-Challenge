<template>
  <div class="mt-3">
    <div class="droptarget">
      <p
        :id="id"
        draggable="true"
        @dragstart="handleDragStart"
        @drag="handleDragging"
        @dragover.prevent
      >
        {{ title }}
      </p>
    </div>
    <!-- <p class="droptarget" @drop="handleDrop" @dragover="allowDrop"></p> -->
    <!-- <span id="demo"></span> -->
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
    type: {
      type: String,
      default: "",
    },
    id: {
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

      countParagraph: 0,
      countButton: 0,
    };
  },
  methods: {
    handleDragStart(event) {
      const target = event.target;
      // console.log('target.id', target.id);
      // event.dataTransfer.setData("Text", target.id);
      event.dataTransfer.setData("drag-id", target.id);
      event.dataTransfer.dropEffect = "move";
      event.dataTransfer.effectAllowed = "move";
      console.log("handleDragStart", event);

      if (target.id === "drag-id-paragraph") {
        const node = document.createElement("p");

        node.addEventListener("click", function handleClickParagraph(event) {
          console.log("element clicked", event);
          document.getElementById("demo-input").innerHTML = "";

          const page = document.createElement("p");
          const input = document.createElement("input");
          page.textContent = "Paragraph Text";
          input.setAttribute("id", "input-paragraph");
          document.getElementById("demo-paragraph").appendChild(page);
          document.getElementById("demo-paragraph").appendChild(input);

          // event handlers input
          const inputParagraph = document.querySelector("#input-paragraph");
          const resultParagraph = document.querySelector("#ele-paragraph");
          inputParagraph.addEventListener("input", function () {
            resultParagraph.textContent = this.value;
          });
        });

        // const textnode = document.createTextNode("Paragraph");
        // node.appendChild(textnode);
        node.textContent = "Paragraph";
        node.setAttribute("id", "ele-paragraph");

        document.getElementById("demo").appendChild(node);
      }

      if (target.id === "drag-id-button"){
        const node = document.createElement("button");

        node.addEventListener("click", function handleClickButton(event) {
          console.log("Button clicked", event);
          document.getElementById("demo-paragraph").innerHTML = "";

          const label1 = document.createElement("p");
          const input1 = document.createElement("input");
          const label2 = document.createElement("p");
          const input2 = document.createElement("input");

          label1.textContent = "Button Text";
          input1.setAttribute("id", "input-button-text");
          label2.textContent = "Alert Message";
          input2.setAttribute("id", "input-alert-message");

          document.getElementById("demo-input").appendChild(label1);
          document.getElementById("demo-input").appendChild(input1);
          document.getElementById("demo-input").appendChild(label2);
          document.getElementById("demo-input").appendChild(input2);

          // event handlers input
          const inputButtonText = document.querySelector("#input-button-text");
          const resultButtonText = document.querySelector("#ele-button");
          inputButtonText.addEventListener("input", function () {
            resultButtonText.textContent = this.value;
          });

          const inputAlertMessage = document.querySelector("#input-alert-message");
          const resultAlertMessage = document.querySelector("#ele-button");
          inputAlertMessage.addEventListener("input", function () {
            // resultButtonText.textContent = this.value;
            console.log('alert message', this.value);
          });
        });

        // const textnode = document.createTextNode("Button");
        // node.appendChild(textnode);
        node.textContent = "Button";
        node.setAttribute("id", "ele-button");

        document.getElementById("demo").appendChild(node);
      }
    },
    handleDragging(event) {
      if (this.title === "Button") {
        this.$emit("dragging", "ElementButton");
        // this.countButton++;
        // console.log('this.countButton', this.countButton);
      } else {
        this.$emit("dragging", "ElementParagraph");
        // this.countParagraph++;
        // console.log('countParagraph', this.countParagraph);
      }
      // document.getElementById("demo").innerHTML =
      //   "The p element is being dragged";
    },
    allowDrop(event) {
      event.preventDefault();
    },
    handleDrop(event) {
      // const target = event.target;
      event.preventDefault();
      // const data = event.dataTransfer.getData("Text");
      // target.appendChild(document.getElementById(data));
      event.dataTransfer.clearData();
      console.log("drop started");
      // document.getElementById("demo").innerHTML = "The p element was dropped";
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

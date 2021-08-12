<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" />
    <div class="drop-zone" @drop="onDrop($event, 1)" @dragenter.prevent @dragover.prevent>
      <div
        v-for="item in getList(1)"
        :key="item.id"
        class="drag-el"
        draggable="true"
        @dragstart="startDrag($event, item)"
      >{{ item.title }}</div>
    </div>
    <div class="drop-zone" @drop="onDrop($event, 2)" @dragenter.prevent @dragover.prevent>
      <div
        v-for="item in getList(2)"
        :key="item.id"
        class="drag-el"
        draggable="true"
        @dragstart="startDrag($event, item)"
      >{{ item.title }}</div>
    </div>
  </div>
</template>

<script lang="ts">
import { ref } from "vue";
import { defineComponent } from "vue";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src

export default defineComponent({
  name: "Home",
  components: {
    HelloWorld,
  },
  setup() {
    const items = ref([
      { id: 0, title: "Item A", list: 1 },
      { id: 1, title: "Item B", list: 1 },
      { id: 2, title: "Item C", list: 2 },
    ]);

    const getList = (list) => {
      return items.value.filter((item) => item.list == list);
    };

    const startDrag = (event, item) => {
      event.dataTransfer.dropEffect = "move";
      event.dataTransfer.effectAllowed = "move";
      event.dataTransfer.setData("itemID", item.id);
    };

    const onDrop = (event, list) => {
      const itemID = event.dataTransfer.getData("itemID");
      const item = items.value.find((item) => item.id == itemID);
      item.list = list;
    };

    return {
      getList,
      startDrag,
      onDrop,
    };
  },
});
</script>
<style scoped>
.drop-zone {
  width: 50%;
  margin: 50px auto;
  background-color: #ecf0f1;
  padding: 10px;
  min-height: 10px;
}

.drag-el {
  background-color: #3498db;
  color: white;
  padding: 5px;
  margin-bottom: 10px;
}

.drga-el:nth-last-of-type(1) {
  margin-bottom: 0;
}
</style>
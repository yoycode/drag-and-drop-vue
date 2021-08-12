<template>
  <div class="about">
    <h1>This is an about pag234234e</h1>
    <TestWorld />
  </div>
</template>
<script>
import { defineComponent } from "vue";
import TestWorld from "@/components/TestWorld.vue";

export default defineComponent({
  name: "About",
  components: {
    TestWorld,
  },
});
</script>

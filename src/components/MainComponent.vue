<template>
  <div class="MainComponent">
    <thermometer />
  </div>
</template>
<script>
import thermometer from "@/components/progressTracking/AppProgress.vue";

export default {
  name: "MainComponent",
  components: {
    thermometer,
  },
};
</script>
<style lang="scss" scoped></style>

<template>
  <div id="app">
    <router-view />
    <FooterComponents />
  </div>
</template>

<script>
import FooterComponents from "@/components/FooterComponents.vue";

export default {
  components: {
    FooterComponents,
  },
};
</script>

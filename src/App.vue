<template>
  <v-app>
    <component :is="layout">
      <router-view :layout.sync="layout" />
    </component>
  </v-app>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      layout: this.$system_config.layoutDefault
    };
  }
};
</script>

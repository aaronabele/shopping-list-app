<template>
  <ListComponent msg="Shopping List App" />
</template>

<script>
import ListComponent from "./components/ListComponent.vue";

export default {
  name: "App",
  components: {
    ListComponent,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  background-color: rgb(212, 235, 243);
}
</style>

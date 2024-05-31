<script>
import AppHeader from './components/AppHeader.vue';

export default {
  name: "App",
  components: {
    AppHeader
  },
  data() {
    return {

    }
  },
  methods: {

  },
  mounted() {
    console.log("App montata");
  }
}
</script>

<template>
  <AppHeader />
  <h2>Film: </h2>
  <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quia, illo!</p>

  <h2>Serie: </h2>
  <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Expedita, repellat?</p>

</template>

<style></style>
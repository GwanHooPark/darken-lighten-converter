<template>
  <div class="home">
    <Convertet />
  </div>
</template>

<script>
// @ is an alias to /src
import Convertet from "@/components/Converter.vue";

export default {
  name: "Home",
  components: {
    Convertet
  }
};
</script>

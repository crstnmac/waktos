<template>
<q-page class="flex flex-center">
  <div>
    <h3 class="text-bold">Pomodro</h3>
    <pomodro />
  </div>
</q-page>
</template>

<script>
import Pomodro from "../components/Pomodro.vue";

export default {
  name: "PageIndex",
  components: {
    Pomodro
  }
};
</script>

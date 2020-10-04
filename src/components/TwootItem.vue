<template>
  <li>{{ userName }}{{ twoot.content }}</li>
</template>

<script>
export default {
  name: "TwootItem",
  props: {
    userName: {
      type: String,
      required: true,
    },
    twoot: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style>
</style>
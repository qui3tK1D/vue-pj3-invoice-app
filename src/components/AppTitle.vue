<template>
  <h1 class="text-center d-print-none">{{ title }}</h1>
  <h1 class="text-center d-none d-print-block">Your Invoice</h1>
</template>

<script>
export default {
  props: {
    title: String,
  },
};
</script>

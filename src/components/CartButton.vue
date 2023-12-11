<template>
  <div
    v-if="addedToCart.length > 0"
    class="fixed bottom-4 flex px-6 items-center justify-center text-white h-10 w-auto whitespace-normal bg-primary rounded-lg right-4 rounded-bl-none"
  >
    You have {{ addedToCart.length }} products in cart
  </div>
</template>

<script lang="ts">
export default {
  components: {},

  props: {
    addedToCart: {
      type: Array,
      required: true,
    },
  },
};
</script>

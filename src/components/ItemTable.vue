<template>
  <div v-if="lists.length">
    <table class="table table-bordered">
      <thead>
        <tr>
          <th>#</th>
          <th>Item</th>
          <th class="text-end">Price</th>
          <th class="text-end">Quantity</th>
          <th class="text-end">Cost</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="({ itemName, price, quantity, cost }, index) in lists"
          :key="index"
          class="animate__animated animate__fadeIn"
        >
          <td>{{ index + 1 }}</td>
          <td class="d-flex justify-content-between">
            {{ itemName }}
            <i
              class="ms-2 bi bi-trash3 text-danger"
              @click="delectItem(index)"
            ></i>
          </td>
          <td class="text-end">{{ price }}</td>
          <td class="text-end">{{ quantity }}</td>
          <td class="text-end">{{ cost }}</td>
        </tr>

        <tr>
          <td colspan="4" class="text-center">Total</td>
          <td class="text-end">{{ totalCost }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    lists: Object,
  },

  computed: {
    totalCost() {
      return this.lists.reduce((acc, cur) => acc + cur.cost, 0);
    },
  },

  methods: {
    delectItem(i) {
      this.$emit("deleteList", i);
    },
  },
};
</script>

<style scoped>
td i:hover {
  cursor: pointer !important;
}
</style>

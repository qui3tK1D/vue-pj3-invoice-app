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
        <TableRow
          v-for="(list, index) in lists"
          :key="index"
          :currentIndex="index"
          :list="list"
          class="animate__animated animate__fadeIn"
          @delItem="del"
        />

        <tr>
          <td colspan="4" class="text-center">Total</td>
          <td class="text-end">{{ totalCost }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import TableRow from "./TableRow.vue";
export default {
  components: {
    TableRow,
  },

  props: {
    lists: Object,
  },

  computed: {
    totalCost() {
      return this.lists.reduce((acc, cur) => acc + cur.cost, 0);
    },
  },

  methods: {
    del(i) {
      this.$emit("deleteList", i);
    },
  },
};
</script>

<style>
td i:hover {
  cursor: pointer !important;
}
</style>

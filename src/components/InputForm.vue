<template>
  <div class="my-4 p-3 border rounded d-print-none">
    <form action="" @submit.prevent="addItem">
      <div class="row g-3">
        <div class="col-md-6">
          <label for="items" class="form-label">Select Item</label>
          <select
            required
            class="form-select"
            id="items"
            v-model="selectedItem"
          >
            <option v-for="item in items" :key="item.id" :value="item.id">
              {{ item.name }}
            </option>
          </select>
        </div>
        <div class="col-md-3">
          <label for="quantity" class="form-label">Quantity</label>
          <input
            required
            type="number"
            class="form-control"
            id="quantity"
            v-model.number="quantity"
          />
        </div>
        <div class="col-md-3 align-self-end">
          <button
            class="btn btn-primary d-flex gap-2 justify-content-center w-100"
          >
            <i class="bi bi-plus-circle text-white"></i>Add Item
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          id: 1,
          name: "Apple",
          price: 50,
        },
        {
          id: 2,
          name: "Orange",
          price: 100,
        },
        {
          id: 3,
          name: "Mango",
          price: 150,
        },
        {
          id: 4,
          name: "Banana",
          price: 30,
        },
      ],
      quantity: 1,
      selectedItem: null,
    };
  },
  methods: {
    addItem() {
      this.$emit(
        "addList",
        this.quantity,
        this.items.find((cur) => cur.id === this.selectedItem)
      );
    },
  },
};
</script>

<style></style>

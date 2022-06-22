<template>
  <div class="container">
    <div class="my-5">
      <AppTitle :title="title" />
      <InputForm @addList="addInvoiceList" />
      <ItemTable :lists="invoiceLists" @deleteList="delInvo" />
      <div class="" v-show="invoiceLists.length">
        <button class="btn btn-outline-primary d-print-none" @click="toPrint">
          Print
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import AppTitle from "./components/AppTitle.vue";
import InputForm from "./components/InputForm.vue";
import ItemTable from "./components/ItemTable.vue";

export default {
  name: "App",
  components: {
    AppTitle,
    InputForm,
    ItemTable,
  },
  data() {
    return {
      title: "Invoice Application",
      invoiceLists: [],
    };
  },
  methods: {
    addInvoiceList(quantity, item) {
      this.invoiceLists = [
        ...this.invoiceLists,
        {
          itemName: item.name,
          price: item.price,
          quantity,
          cost: item.price * quantity,
        },
      ];
    },
    delInvo(index) {
      this.invoiceLists = [...this.invoiceLists.filter((_, i) => i !== index)];
    },
    toPrint() {
      print();
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@200;300;400;500&family=Padauk:wght@400;700&display=swap");

@import "bootstrap-icons/font/bootstrap-icons.css";
@import "animate.css/animate.min.css";
@import "bootstrap/dist/css/bootstrap.min.css";

* {
  font-family: "Montserrat", sans-serif;
  color: #2c3e50;
}
</style>

<template>
  <tr>
    <td>{{ currentIndex + 1 }}</td>
    <td>
      <div class="d-flex justify-content-between">
        <span>{{ list.itemName }}</span>
        <div
          v-if="isDelecting"
          class="spinner-border spinner-border-sm text-danger"
          role="status"
        >
          <span class="visually-hidden">Loading...</span>
        </div>
        <i
          v-else
          class="ms-2 bi bi-trash3 text-danger"
          @click="delectItem(currentIndex)"
        ></i>
      </div>
    </td>
    <td class="text-end">{{ list.price }}</td>
    <td class="text-end">{{ list.quantity }}</td>
    <td class="text-end">{{ list.cost }}</td>
  </tr>
</template>

<script>
import Swal from "sweetalert2";
export default {
  props: {
    list: Object,
    currentIndex: Number,
  },
  data() {
    return {
      isDelecting: false,
    };
  },
  methods: {
    delectItem(currentIndex) {
      Swal.fire({
        title: "Are you sure?",
        text: "You won't be able to revert this!",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#3085d6",
        cancelButtonColor: "#d33",
        confirmButtonText: "Yes, delete it!",
      }).then((result) => {
        this.isDelecting = true;
        if (result.isConfirmed) {
          setTimeout(() => {
            this.$emit("delItem", currentIndex);
            this.isDelecting = false;

            const Toast = Swal.mixin({
              toast: true,
              position: "top-end",
              showConfirmButton: false,
              timer: 2000,
              timerProgressBar: true,
              didOpen: (toast) => {
                toast.addEventListener("mouseenter", Swal.stopTimer);
                toast.addEventListener("mouseleave", Swal.resumeTimer);
              },
            });
            Toast.fire({
              icon: "success",
              title: "deleted successfully",
            });
          }, 500);
        } else {
          this.isDelecting = false;
        }
      });
    },
  },
};
</script>

<style></style>

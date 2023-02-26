<template>
  <div class="mymodal">
    <!-- Button trigger modal -->
    <button
      type="button"
      class="btn btn-warning btn-sm"
      data-bs-toggle="modal"
      :data-bs-target="'#' + modalId"
    >
      Edit
    </button>

    <!-- Modal -->
    <div
      class="modal fade"
      :id="modalId"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="exampleModalLabel">
              Edit a Task!
            </h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <div class="form-floating mb-3">
              <input
                v-model="editedTitle"
                type="text"
                class="form-control"
                id="floatingInput"
                placeholder="text"
              />
              <label for="floatingInput">Task Title</label>
            </div>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
            <button
              type="button"
              class="btn btn-success"
              @click="updateTask"
              data-bs-dismiss="modal"
            >
              Edit
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      required: true,
    },
    modalId: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      editedTitle: this.task.title,
    };
  },
  methods: {
    updateTask() {
      this.$emit("update-task", {
        editedTitle: this.editedTitle,
        taskTitle: this.task.title,
      });
    },
  },
};
</script>

<style></style>

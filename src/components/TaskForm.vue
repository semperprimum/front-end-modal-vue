<template>
  <div class="container d-flex justify-content-between align-items-center">
    <HeaderView />
    <div class="mymodal">
      <!-- Button trigger modal -->
      <button
        type="button"
        class="btn btn-success btn__add-task btn-lg"
        data-bs-toggle="modal"
        data-bs-target="#taskForm"
      >
        Add
      </button>

      <!-- Modal -->
      <div
        class="modal fade"
        id="taskForm"
        tabindex="-1"
        aria-labelledby="exampleModalLabel"
        aria-hidden="true"
      >
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h1 class="modal-title fs-5" id="exampleModalLabel">
                Add a Task!
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
                  v-model="task.title"
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
                @click="addTask"
                type="button"
                class="btn btn-success"
                data-bs-dismiss="modal"
              >
                Add
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HeaderView from "./HeaderView.vue";
export default {
  name: "TaskForm",
  components: {
    HeaderView,
  },
  data() {
    return {
      task: {
        title: "",
      },
    };
  },
  methods: {
    addTask() {
      this.task.id = Date.now();
      this.$emit("addTask", this.task);
      this.task = {
        title: "",
      };
    },
  },
};
</script>

<style scoped></style>

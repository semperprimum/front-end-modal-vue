<template>
  <table class="table">
    <thead>
      <tr>
        <th>Task</th>
        <th></th>
        <th></th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="task in tasks" :key="task.id">
        <td>{{ task.title }}</td>
        <td>
          <EditModal
            :task="task"
            :modalId="'editModal' + task.id"
            @update-task="onUpdateTask(task.id, $event)"
          />
        </td>
        <td>
          <button class="btn btn-danger btn-sm" @click="$emit('delete', task)">
            Delete
          </button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import EditModal from "@/components/EditModal";
export default {
  components: {
    EditModal,
  },
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
  methods: {
    onUpdateTask(taskId, payload) {
      this.$emit("update-task", { taskId, ...payload });
    },
  },
};
</script>

<style scoped></style>

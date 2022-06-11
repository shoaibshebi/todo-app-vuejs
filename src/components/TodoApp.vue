<template>
  <div class="container">
    <h2 class="text-center mt-5">Vue Todo Application</h2>
    <div class="d-flex">
      <input
        type="text"
        v-model="task"
        placeholder="Enter task"
        class="form-control"
      />
      <button @click="submitTask" class="btn btn-warning">ADD</button>
    </div>

    <table class="table table-bordered mt-5 rounded-2">
      <thead>
        <tr>
          <!-- {{msg}} -->
          <th scope="col">Task</th>
          <th scope="col" style="width: 120px">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task.name }}</td>
          <td>{{ task.status }}</td>
          <td class="text-center">
            <div @click="editTask(index)">
              <p class="fa fa-pen pointer"></p>
            </div>
          </td>
          <td class="text-center">
            <div @click="deleteTask(index)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "TodoApp",
  props: {
    msg: String,
  },
  data() {
    return {
      task: "",
      isEditable: null,
      tasks: [
        {
          name: "Steal banans from teh store",
          status: "to-do",
        },
        {
          name: "Eat cho in 1 hour",
          status: "in-progress",
        },
      ],
    };
  },
  methods: {
    submitTask() {
      if (this.task.length === 0) return;
      if (this.isEditable === null) {
        this.tasks.push({
          name: this.task,
          status: "to-do",
        });
      } else {
        this.tasks[this.isEditable].name = this.task;
        this.isEditable = null;
      }
      this.task = "";
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].name;
      this.isEditable = index;
    },
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
</style>

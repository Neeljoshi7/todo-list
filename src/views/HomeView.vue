<template>
  <div class="w-50 mx-auto my-5">
    <button
      type="button"
      @click="this.$router.push('/addTodo')"
      class="btn btn-success ms-2"
    >
      Add Todo
    </button>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Task Name</th>
          <th scope="col">Priority</th>
          <th scope="col">Status</th>
          <th scope="col">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in getTodo" :key="index">
          <th scope="row">
            <div class="check-box">
              <input
                type="checkbox"
                v-if="todo.status == 'Pending'"
                @change="changeStatus(todo.id)"
              />
               <input
                type="checkbox"
                checked
                v-if="todo.status == 'Done'"
                @change="changeStatus(todo.id)"
              />
            </div>
          </th>
          <td :class="{ 'task-done': todo.status == 'Done' }">
            {{ todo.newTask }}
          </td>
          <td  :class="{ 'task-done': todo.status == 'Done' }">{{ todo.priority }}</td>
          <td>{{ todo.status }}</td>
          <td>
            <button
              @click="editTask(todo)"
              type="button"
              class="btn btn-primary"
            >
              Edit</button
            ><button
              type="button"
              class="btn btn-danger ms-2"
              @click="delTodo(todo.id)"
            >
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      getTodo: [],
      demo: {
        name: "Hello World",
      },
    };
  },
  mounted() {
    this.getTodo = JSON.parse(localStorage.getItem("newTodos"));
  },
  methods: {
    editTask(i) {
      // console.log('Neel',i);
      this.$router.push({
        path: "/edittask",
        query: {
          id: i.id,
          name: i.newTask,
          priority: i.priority,
          status: i.status,
        },
      });
    },
    delTodo(item) {
      let updat = this.getTodo.filter((todo) => todo.id !== item);
      this.getTodo = updat;
      localStorage.setItem("newTodos", JSON.stringify(updat));
    },
    changeStatus(id) {
      let edit = this.getTodo.find((todo) => todo.id == id);
      if (edit.status == "Pending") {
        edit.status = "Done";
      } else {
        edit.status = "Pending";
      }
      localStorage.setItem("newTodos", JSON.stringify(this.getTodo));
    },
  },
};
</script>

<style scoped>
.check-box {
  transform: scale(1.5);
}

input[type="checkbox"] {
  position: relative;
  appearance: none;
  width: 20px;
  height: 10px;
  background: #ccc;
  border-radius: 50px;
  box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
  cursor: pointer;
  transition: 0.4s;
}

input:checked[type="checkbox"] {
  background: #7da6ff;
}

input[type="checkbox"]::after {
  position: absolute;
  content: "";
  width: 10px;
  height: 10px;
  top: 0;
  left: 0;
  background: #fff;
  border-radius: 50%;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
  transform: scale(1.1);
  transition: 0.4s;
}

input:checked[type="checkbox"]::after {
  left: 50%;
}
</style>
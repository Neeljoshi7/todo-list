<template>
  <div class="addtask-form">
    <form @submit.prevent="addTodo">
      <h1 class="text-center">Todo form</h1>
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label text-dark"
          >Enter Task :</label
        >
        <input
          type="text"
          class="form-control"
          id="exampleInputEmail1"
          aria-describedby="emailHelp"
          v-model="addNewTodo.newTask"
        />
      </div>
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label text-dark"
          >Priority :</label
        >
        <select
          class="form-select"
          v-model="addNewTodo.priority"
          aria-label="Default select example"
        >
          <option selected>All</option>
          <option value="High">High</option>
          <option value="Medium">Medium</option>
          <option value="Low">Low</option>
        </select>
      </div>
      <button type="submit" class="btn btn-dark w-100">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      addNewTodo: {
        id: "",
        newTask: "",
        priority: "",
        status: "Pending",
      },
      newTodos: [],
    };
  },
  methods: {
    addTodo() {
      let exist = JSON.parse(localStorage.getItem("newTodos"));
      if (exist.length>0) {
        // console.log(exist[0].id)
        this.newTodos.push({
          id: exist[0].id+1,
          newTask: this.addNewTodo.newTask,
          priority: this.addNewTodo.priority,
          status: this.addNewTodo.status,
        });
      } else {
        this.newTodos.push({
          id: 0,
          newTask: this.addNewTodo.newTask,
          priority: this.addNewTodo.priority,
          status: this.addNewTodo.status,
        });
      }
      if (exist.length>0) {
        localStorage.setItem(
          "newTodos",
          JSON.stringify([...this.newTodos, ...exist])
        );
      } else {
        localStorage.setItem("newTodos", JSON.stringify([...this.newTodos]));
      }
      this.$router.push("/");
    },
  },
};
</script>

<style>
.addtask-form {
  width: 25%;
  margin: 10% auto;
  border: 1px solid black;
  padding: 40px;
  border-radius: 13px;
}
</style>

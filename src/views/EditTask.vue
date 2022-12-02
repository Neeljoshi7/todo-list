<template>
  <div>
    <div class="addtask-form">
      <form @submit.prevent="editTask">
        <h1 class="text-center">Edit task form</h1>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label text-dark"
            >Edit Task :</label
          >
          <input
            type="text"
            class="form-control"
            id="exampleInputEmail1"
            aria-describedby="emailHelp"
            v-model="name"
          />
        </div>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label text-dark"
            >Priority :</label
          >
          <select
            class="form-select"
            aria-label="Default select example"
            v-model="priority"
          >
            <option
              v-for="option in options"
              :key="option.value"
              :value="option.value"
            >
              {{ option.value }}
            </option>
          </select>
        </div>
        <button type="submit" class="btn btn-dark">Save Changes</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      getObj: [],
      options: [
        {
          value: "High",
        },
        {
          value: "Medium",
        },
        {
          value: "Low",
        },
      ],
      name: "",
      priority: "",
    };
  },
  mounted() {
    this.getObj = this.$route.query;
    console.log("Hello", this.getObj);
    console.log(this.getObj.priority);
    this.name = this.getObj.name;
    this.priority = this.getObj.priority;
  },
  methods: {
    editTask() {
      var exist = JSON.parse(localStorage.getItem("newTodos"));
      var edit = exist.find((todo) => todo.id == this.getObj.id);
      edit.newTask = this.name;
      edit.priority = this.priority;

      localStorage.setItem("newTodos", JSON.stringify(exist));
      this.$router.push("/");
      console.log(exist);
    },
    handleChange(i) {
      this.getObj = i.target.value;
      console.log("this.getObj", this.getObj);
      console.log("i", i.target.val);
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
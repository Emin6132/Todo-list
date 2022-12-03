<template>
  <div id="app">
    <div class="container" id="app">
      <div class="card">
        <div class="card-header">
          <h4>To Do List</h4>
        </div>
        <div class="card-body">
          <div class="input-container">
            <input
              type="text"
              name="Todo"
              placeholder="Whats needs to be add"
              class="form-control"
              v-model="message"
              @keyup.enter="add"
            />
          </div>
          <div class="list-group">
            <li
              class="list-group-item"
              v-for="(list, index) in lists"
              :key="list"
            >
              <span class="message">{{ list }}</span>
              <button class="btn btn-danger" @click="remove(index)">
                Delete
              </button>
            </li>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      message: "",
      editing: false,
      editingId: 0,
      lists: [],
    };
  },
  mounted() {
    if (localStorage.lists) {
      this.lists = JSON.parse(localStorage.lists);
    }
  },
  watch: {
    lists: {
      handler(message) {
        localStorage.lists = JSON.stringify(message);
      },
      deep: true,
    },
  },
  methods: {
    add: function () {
      if (this.message !== "") {
        if (this.editing) {
          this.lists[this.editingId] = this.message;
          (this.message = ""), (this.editingId = false);
        } else {
          this.lists.push(this.message), (this.message = "");
        }
      }
    },
    remove: function (index) {
      this.lists.splice(index, 1);
    },
  },
};
</script>
<style>
body {
  background-color: mintcream;
}
.container {
  display: flex;
  justify-content: center;
  box-shadow: 1px 1px 10px 4px lightgray;
  margin: auto;
  margin-top: 80px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  width: 500px;
  height: 400px;
  background-color: white;
}
.card-header {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 60px;
  font-size: 24px;
}
.card-body {
  justify-content: space-around;
  height: 80%;
  width: 80%;
  display: flex;
  flex-direction: column;
}
.form-control {
  text-align: center ;
  border-radius: 4px;
  border: none;
  box-shadow: 1px 1px 10px 4px lightgray;
  height: 30px;
  width: 300px;
}
.list-group {
  width: 305px;
  overflow-y: auto;
  height: 600px;
  margin-top: 20px;
}
.list-group-item {
  margin-bottom: 10px;
  align-items: center;
  height: 50px;
  border: 1px solid black;
  border-radius: 4x;
  justify-content: space-between;
  width: 302px;
  display: flex;
  list-style: none;
  border-radius: 4px;
}
.message {
  margin-left: 10px;
}
.btn {
  margin-right: 10px;
  background-color: tomato;
  cursor: pointer;
  border: none;
  border-radius: 3px;
  color: white;
  height: 30px;
}
</style>

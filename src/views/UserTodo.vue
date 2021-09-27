<template>
  <div class="user-todo">
    <h1>{{ userData.name }}</h1>
    <h6>{{ userData.email }}</h6>
    <div
      v-for="todo in userData.todos"
      :key="todo.id"
      class="card my-3 bg-dark shadow-sm"
    >
      <div class="card-body">
        <main class="d-flex justify-content-between align-items-center">
          <div>
            <h4 :class="[todo.user_done ? 'text-decoration-line-through' : '' , 'text-light mb-0']">{{ todo.title }}</h4>
            <p class="text-secondary">{{ todo.description }}</p>
          </div>
          <div>
              <span v-if="todo.user_done" class="text-success fs-1"><i class="bi bi-check-square"></i></span>
              <span v-else class="text-light fs-1"><i class="bi bi-square"></i></span>
              <!-- <p class="text-warning"> {{todo.user_done}}</p> -->
          </div>
        </main>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "user-todo",
  data() {
    return {
      userData: [],
    };
  },
  created() {
    const userId = this.$route.params.id;
    fetch("http://127.0.0.1:8000/api/users/" + userId)
      .then((res) => res.json())
      .then((r) => {
        this.userData = r.data;
      });
  },
};
</script>

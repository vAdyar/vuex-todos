<template>
  <div class="home">
    <div class="container">
      <AddTodo/>

      <Todos/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Todos from "@/components/Todos.vue";
import AddTodo from "@/components/AddTodo.vue";

export default {
  name: "Home",
  components: {
    Todos,
    AddTodo
  }
};
</script>

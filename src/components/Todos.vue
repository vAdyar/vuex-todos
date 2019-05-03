<template>
    <div>
        <h3>Todos</h3>
        <FilterTodo />
        <div class="legend">
            <span> Double click to mark as completed</span>
            <span>
                <span class="incompleted-box"></span> = Incompleted
             </span>
            <span>
                <span class="completed-box"></span> = Completed
             </span>
        </div>
        <div class="todos">
            <div @dblclick="completed(todo)" v-for="todo in allTodos" :key="todo.id" class="todo" v-bind:class="{'is-complete':todo.completed}">
                {{ todo.title }}
                <i @click="deleteTodo(todo.id)" class="fas fa-trash-alt"></i>
            </div>
        </div>
    </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
import FilterTodo from "@/components/FilterTodo.vue";

export default {
  name: 'Todos',
  components: {
      FilterTodo
  },
  methods: {
      ...mapActions(['fetchTodos', 'deleteTodo', 'updateTodo']),
      completed(todo) {
          const updTodo = {
              id: todo.id,
              title: todo.title,
              completed: !todo.completed
          }
          this.updateTodo(updTodo);
      } 
  },
  computed: mapGetters([ 'allTodos']),
  created() {
      this.fetchTodos();
  }
}
</script>

<style>
body {
    line-height: 1.6;
    background: #e8f7f0
}

.container {
    max-width: 1100px;
    margin: auto;
    overflow: auto;
    padding: 0 2rem;
}

.todos {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 1rem;
}

.todo {
    border: 1px solid #ccc;
    background: #41b883;
    padding: 1rem;
    border-radius: 5px;
    text-align: center;
    position: relative;
    cursor: pointer;
}

i {
    position: absolute;
    bottom: 10px;
    right: 10px;
    color: #fff;
    cursor: pointer;
}

.legend {
    display: flex;
    justify-content: space-around;
    margin-bottom: 1rem;
}

.completed-box {
    display: inline-block;
    width: 10px;
    height: 10px;
    background: #35495e
}

.incompleted-box {
    display: inline-block;
    width: 10px;
    height: 10px;
    background: #41b883
}

@media (max-width: 500px) {
    .todo {
        grid-template-columns: 1fr;
    }
}

.is-complete {
    background: #35495e;
    color:#ccc
}
</style>

<script>
import CreateForm from "./addForm/CreateForm.vue";
import EditForm from "./editForm/EditForm.vue";
import Todo from "./listItem/Todo.vue";
export default {
  components: {
    CreateForm,
    EditForm,
    Todo,
  },
  emits: ["addTodo", "editTodo", "deleteTodo"],
  props: {
    selectedProject: {
      type: Object,
    },
  },
  data: () => ({
    isFormOpened: false,
  }),
  methods: {
    openForm() {
      if (this.selectedProject.id) {
        this.isFormOpened = true;
      } else {
        alert("Please select project");
      }
    },
    closeForm() {
      this.isFormOpened = false;
    },
  },
};
</script>

<template>
  <div class="flex flex-col items-center py-2 px-10">
    <button
      @click="openForm"
      class="px-4 py-2 text-2xl w-full font-bold hover:bg-red-400 rounded-xl cursor-pointer duration-300"
    >
      + New todo
    </button>
    <CreateForm
      v-if="isFormOpened && selectedProject.id"
      @closeForm="$emit('closeForm')"
      @addTodo="$emit('addTodo', $event)"
      :selectedProjectId="selectedProject.id"
    />
    <h1 v-if="selectedProject.id" class="text-xl font-medium mt-2">Todos:</h1>
    <ul class="w-full flex flex-col gap-2 mt-2">
      <template v-for="todo in selectedProject.todos" :key="todo.id">
        <Todo
          v-if="!todo.isEditing"
          :selectedProjectId="selectedProject.id"
          :todo="todo"
          @deleteTodo="$emit('deleteTodo', $event)"
          @edit="todo.isEditing = true"
        />
        <EditForm
          v-else
          :todo="todo"
          :selectedProjectId="selectedProject.id"
          @edit="todo.isEditing = false"
          @editTodo="$emit('editTodo', $event)"
          @deleteTodo="$emit('deleteTodo', $event)"
        />
      </template>
    </ul>
  </div>
</template>

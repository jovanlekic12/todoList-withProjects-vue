<script>
export default {
  props: {
    deleteTodo: {
      type: Function,
      required: true,
    },
    editTodo: {
      type: Function,
      required: true,
    },
    selectedProjectId: {
      type: String,
      required: true,
    },
    todo: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      newTodo: {
        id: this.todo.id,
        title: this.todo.title,
        date: this.todo.date,
        isChecked: this.todo.isChecked,
        isEditing: false,
      },
    };
  },
  methods: {
    handleEdit() {
      this.editTodo(this.selectedProjectId, this.newTodo);
    },
  },
};
</script>
<template>
  <div class="flex items-center justify-between w-full">
    <div class="flex items-center gap-6">
      <h1 class="text-2xl font-semibold">Title:</h1>
      <input
        type="text"
        v-model="newTodo.title"
        class="text-base px-3 py-1 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-red-400"
      />
    </div>
    <div class="flex items-center gap-6">
      <h1 class="text-2xl font-semibold">Date:</h1>
      <input
        type="date"
        v-model="newTodo.date"
        class="text-base px-3 py-1 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-red-400"
      />
    </div>
    <div class="flex items-center gap-4">
      <button
        @click="handleEdit"
        class="text-lg uppercase font-semibold px-4 py-1 rounded-xl border border-gray-400 cursor-pointer"
      >
        edit
      </button>
      <button
        @click="deleteTodo(selectedProjectId, todo.id)"
        class="text-lg uppercase font-semibold px-4 py-1 rounded-xl border border-gray-400 cursor-pointer"
      >
        delete
      </button>
    </div>
    <input
      type="checkbox"
      v-model="newTodo.isChecked"
      class="w-8 h-8 accent-red-500 cursor-pointer"
    />
  </div>
</template>

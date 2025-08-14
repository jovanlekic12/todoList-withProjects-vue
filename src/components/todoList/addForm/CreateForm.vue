<script>
export default {
  props: {
    closeForm: {
      type: Function,
      required: true,
    },
    addTodo: {
      type: Function,
      required: true,
    },
    selectedProjectId: {
      type: String,
      required: true,
    },
  },
  methods: {
    submitForm() {
      if (this.todo.title.trim() && this.todo.date)
        this.addTodo(this.selectedProjectId, this.todo);
      this.closeForm();
    },
  },
  data: () => ({
    todo: {
      id: self.crypto.randomUUID(),
      title: "",
      date: "",
      isEditing: false,
      isChecked: false,
    },
  }),
};
</script>
<template>
  <form class="w-3/5 flex flex-col mt-5" @submit.prevent="submitForm">
    <div
      class="flex items-center justify-between bg-red-300 px-5 py-2 rounded-xl"
    >
      <div class="flex items-center gap-2">
        <label class="text-xl">Title:</label>
        <input
          v-model="todo.title"
          type="text"
          placeholder="My todo"
          class="bg-white px-2 py-1 rounded-lg text-sm"
          required
        />
      </div>
      <div class="flex items-center gap-2">
        <label class="text-xl">Date:</label>
        <input
          type="date"
          v-model="todo.date"
          class="bg-white px-2 py-1 rounded-lg text-sm"
          required
        />
      </div>
    </div>
    <div class="flex items-center gap-3 mt-3">
      <button
        type="submit"
        class="bg-green-300 w-full text-2xl font-bold py-1.5 rounded-xl cursor-pointer"
      >
        Add
      </button>
      <button
        @click="closeForm"
        class="bg-red-400 w-full text-2xl font-bold py-1.5 rounded-xl cursor-pointer"
      >
        Cancel
      </button>
    </div>
  </form>
</template>

<script>
export default {
  emits: ["deleteTodo"],
  props: {
    selectedProjectId: {
      type: String,
    },
    todo: {
      type: Object,
      required: true,
    },
  },
};
</script>
<template>
  <li class="flex items-center justify-between bg-red-200 p-4 rounded-xl">
    <div class="flex items-center justify-between w-full">
      <div class="flex items-center gap-2">
        <h1 class="text-xl font-medium">Title:</h1>
        <p class="text-xl">{{ todo.title }}</p>
      </div>

      <div class="flex items-center gap-2">
        <h1 class="text-xl font-medium">Date:</h1>
        <p class="text-xl">{{ todo.date }}</p>
      </div>

      <div class="flex items-center gap-8">
        <button
          class="text-lg uppercase font-semibold px-4 py-1 rounded-xl border border-gray-400 cursor-pointer"
          @click="$emit('edit', todo.id)"
        >
          edit
        </button>
        <button
          @click="$emit('deleteTodo', todo.id)"
          class="text-lg uppercase font-semibold px-4 py-1 rounded-xl border border-gray-400 cursor-pointer"
        >
          delete
        </button>
      </div>
      <input type="checkbox" class="w-7 h-7" v-model="todo.isChecked" />
    </div>
  </li>
</template>

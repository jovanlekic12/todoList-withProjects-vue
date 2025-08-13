<script>
export default {
  props: {
    closeForm: {
      type: Function,
      required: true,
    },
  },
};
</script>
<template>
  <form class="w-3/5 flex flex-col mt-5">
    <div
      class="flex items-center justify-between bg-red-300 px-5 py-2 rounded-xl"
    >
      <div class="flex items-center gap-2">
        <label class="text-xl">Title:</label>
        <input
          type="text"
          placeholder="My todo"
          class="bg-white px-2 py-1 rounded-lg text-sm"
        />
      </div>
      <div class="flex items-center gap-2">
        <label class="text-xl">Date:</label>
        <input type="date" class="bg-white px-2 py-1 rounded-lg text-sm" />
      </div>
    </div>
    <div class="flex items-center gap-3 mt-3">
      <button
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

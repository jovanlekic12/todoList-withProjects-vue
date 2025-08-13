<script>
export default {
  props: {
    closeForm: {
      type: Function,
      required: true,
    },
    addProject: {
      type: Function,
      required: true,
    },
  },
  data: () => ({
    projectName: "",
  }),
  methods: {
    submitForm() {
      if (this.projectName.trim()) {
        this.addProject(this.projectName.trim());
        this.projectName = "";
        this.closeForm();
      }
    },
  },
};
</script>

<template>
  <form class="w-3/4 mt-5" @submit.prevent="submitForm">
    <input
      v-model="projectName"
      type="text"
      placeholder="Project name"
      class="w-full rounded-xl bg-white px-3 py-1"
    />
    <div class="flex items-center justify-between px-3 mt-2">
      <button
        type="submit"
        class="bg-white cursor-pointer px-3 py-1 text-xl uppercase font-medium rounded-xl"
      >
        Add
      </button>
      <button
        type="button"
        @click="closeForm"
        class="bg-white cursor-pointer px-3 py-1 text-xl uppercase font-medium rounded-xl"
      >
        Cancel
      </button>
    </div>
  </form>
</template>

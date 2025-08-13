<script>
import CreateForm from "./addForm/CreateForm.vue";
export default {
  components: {
    CreateForm,
  },
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
      :closeForm="closeForm"
    />
    <h1 v-if="selectedProject.id" class="text-xl font-medium mt-2">Todos:</h1>
  </div>
</template>

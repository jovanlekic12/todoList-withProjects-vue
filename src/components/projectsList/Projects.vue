<script>
import ProjectForm from "./form/ProjectForm.vue";
export default {
  components: {
    ProjectForm,
  },
  props: {
    projects: {
      type: Array,
      required: true,
    },
    addProject: {
      type: Function,
      required: true,
    },
    deleteProject: {
      type: Function,
      required: true,
    },
    selectProject: {
      type: Function,
      required: true,
    },
    selectedProjectId: {
      type: String,
    },
  },
  data: () => ({
    isFormOpened: false,
  }),
  methods: {
    openForm() {
      this.isFormOpened = true;
    },
    closeForm() {
      this.isFormOpened = false;
      console.log(this.projects);
    },
  },
};
</script>

<template>
  <div class="flex flex-col items-center bg-red-300 py-2 px-4 h-dvh">
    <button
      class="px-4 py-2 text-2xl w-full font-bold hover:bg-red-600 rounded-xl cursor-pointer duration-300"
      @click="openForm"
    >
      + New project
    </button>
    <ProjectForm
      v-if="isFormOpened"
      :closeForm="closeForm"
      :addProject="addProject"
    />
    <h1 v-if="projects.length > 0" class="text-xl font-medium mt-2">
      Projects:
    </h1>
    <ul class="w-full px-5 mt-5 flex flex-col gap-5">
      <li
        :key="`project-${project.id}`"
        v-for="project in projects"
        @click="selectProject(project.id)"
        :class="[
          'flex items-center justify-between w-full font-bold hover:bg-red-600 duration-300 cursor-pointer px-5 py-2 rounded-xl',
          project.id === selectedProjectId ? 'bg-red-800 text-white' : '',
        ]"
      >
        <p>{{ project.name }}</p>
        <button class="cursor-pointer" @click.stop="deleteProject(project.id)">
          X
        </button>
      </li>
    </ul>
  </div>
</template>

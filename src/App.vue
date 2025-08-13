<script>
import Projects from "./components/projectsList/Projects.vue";
import Todos from "./components/todoList/Todos.vue";
export default {
  components: {
    Projects,
    Todos,
  },
  data: () => ({
    projects: [],
    selectedProject: {},
  }),
  methods: {
    addProject(projectName) {
      this.projects.push({
        id: self.crypto.randomUUID(),
        name: projectName,
        todos: [],
      });
    },
    deleteProject(projectId) {
      this.projects = this.projects.filter(
        (project) => project.id !== projectId
      );
      if (projectId === this.selectedProject.id) {
        this.selectedProject = {};
      }
    },
    selectProject(projectId) {
      this.selectedProject = this.projects.find(
        (project) => project.id === projectId
      );

      console.log(this.selectedProject, "brao");
    },
  },
};
</script>

<template>
  <header class="w-full bg-pink-900 px-3 py-4">
    <h1 class="text-5xl font-bold text-white">TODO LIST</h1>
  </header>
  <main class="grid grid-cols-[500px_minmax(900px,_1fr)]">
    <Projects
      :projects="projects"
      :addProject="addProject"
      :deleteProject="deleteProject"
      :selectProject="selectProject"
      :selectedProjectId="selectedProject.id"
    />
    <Todos :selectedProject="selectedProject" />
  </main>
</template>

<style scoped></style>

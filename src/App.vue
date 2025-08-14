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
    addTodo(selectedProjectId, todo) {
      const newProjects = this.projects.map((project) => {
        return project.id === selectedProjectId
          ? { ...project, todos: [...project.todos, todo] }
          : project;
      });
      this.projects = newProjects;
      this.selectedProject.todos.push(todo);
    },
    deleteTodo(selectedProjectId, todoId) {
      const newProjects = this.projects.map((project) => {
        return project.id === selectedProjectId
          ? {
              ...project,
              todos: project.todos.filter((todo) => todo.id !== todoId),
            }
          : project;
      });
      this.projects = newProjects;
      this.selectedProject.todos = this.selectedProject.todos.filter(
        (todo) => todo.id !== todoId
      );
    },
    editTodo(projectId, newTodo) {
      const newProjects = this.projects.map((project) => {
        return project.id === projectId
          ? {
              ...project,
              todos: project.todos.map((todo) => {
                return todo.id === newTodo.id
                  ? { ...todo, ...newTodo }
                  : { ...todo };
              }),
            }
          : project;
      });
      const newTodos = this.selectedProject.todos.map((todo) => {
        return todo.id === newTodo.id ? { ...todo, ...newTodo } : { ...todo };
      });
      this.projects = newProjects;
      this.selectedProject.todos = newTodos;
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
    <Todos
      :selectedProject="selectedProject"
      :addTodo="addTodo"
      :deleteTodo="deleteTodo"
      :editTodo="editTodo"
    />
  </main>
</template>

<style scoped></style>

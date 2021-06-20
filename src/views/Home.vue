<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject
          :project="project"
          @deleteProject="handleDelete"
          @toggleComplete="handleComplete"
        />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from "../components/SingleProject.vue";
export default {
  name: "Home",
  components: { SingleProject },
  data() {
    return {
      projects: [],
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      });
    },
    handleComplete(id) {
      this.projects = this.projects.map((project) => {
        if (project.id === id) {
          project.completed = !project.completed;
        }
        return project;
      });
    },
  },
};
</script>

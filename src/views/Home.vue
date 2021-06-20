<template>
  <div class="home">
    <FilterNav @updateFilter="handleFilter" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
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
import FilterNav from "../components/FilterNav.vue";
export default {
  name: "Home",
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: "all",
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
    handleFilter(by) {
      console.log(by);
      this.current = by;
    },
  },
  computed: {
    filteredProjects() {
      if (this.current == "completed") {
        return this.projects.filter((project) => project.completed);
      } else if (this.current == "ongoing") {
        return this.projects.filter((project) => !project.completed);
      }
      return this.projects;
    },
  },
};
</script>

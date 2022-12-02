<template>
  <h1>Home</h1>
  <FilterNav @filterBy="current = $event" :current="current" />
  <div v-for="project in filteredProjects" :key="project.id">
    <SingleProject
      :project="project"
      @delete="deleteProject"
      @complete="completeProject"
    ></SingleProject>
  </div>
</template>

<script>
import FilterNav from "../components/FilterNav.vue";
import SingleProject from "../components/SingleProject.vue";
export default {
  name: "HomeView",
  components: {
    SingleProject,
    FilterNav,
  },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  methods: {
    deleteProject(id) {
      this.projects = this.projects.filter((project) => {
        return project.id != id;
      });
    },
    completeProject(id) {
      let findProject = this.projects.find((project) => {
        return project.id === id;
      });
      findProject.complete = !findProject.complete;
    },
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => {
        return res.json();
      })
      .then((datas) => {
        this.projects = datas;
      })
      .catch((err) => {
        console.log(err.message());
      });
  },
  computed: {
    filteredProjects() {
      if (this.current === "complete") {
        return this.projects.filter((project) => {
          return project.complete;
        });
      }
      if (this.current === "ongoing") {
        return this.projects.filter((project) => {
          return !project.complete;
        });
      }
      return this.projects;
    },
  },
};
</script>
<style>
h2 {
  margin-left: 20px;
}
</style>
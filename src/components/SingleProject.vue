<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="d-flex">
      <h5 @click="showDetail = !showDetail">{{ project.title }}</h5>
      <div>
        <i class="fa-solid fa-trash" @click="deleteProject"></i>
        <router-link :to="{ name: 'editProject', params: { id: project.id } }">
          <i class="fa-solid fa-pen"></i>
        </router-link>
        <i class="fa-sharp fa-solid fa-check" @click="completeProject"></i>
      </div>
    </div>
    <p v-if="showDetail">{{ project.detail }}</p>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetail: false,
      api: "http://localhost:3000/projects/",
    };
  },
  methods: {
    deleteProject() {
      let deleteRoute = this.api + this.project.id;
      fetch(deleteRoute, { method: "DELETE" })
        .then(() => {
          this.$emit("delete", this.project.id);
        })
        .catch((err) => {
          console.log(err.message());
        });
    },
    completeProject() {
      fetch(this.api + this.project.id, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          complete: !this.project.complete,
        }),
      })
        .then(() => {
          this.$emit("complete", this.project.id);
        })
        .catch((err) => {
          console.log(err.message);
        });
    },
  },
};
</script>

<style>
.project {
  background-color: #eee;
  padding: 15px;
  margin: 20px;
  border-radius: 10px;
  border-left: 6px solid crimson;
}
.d-flex {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.d-flex i {
  font-size: 18px;
  margin-left: 15px;
  cursor: pointer;
  transition: 0.5s;
}
.d-flex i:hover {
  color: crimson;
}
h5 {
  font-family: sans-serif;
  font-size: 22px;
  cursor: pointer;
  color: indigo;
}
.d-flex a {
  color: black;
}
.complete {
  border-left-color: green;
}
</style>
<template>
  <h2>Add Project</h2>
  <form @submit.prevent="submit">
    <div>
      <label>Title</label>
      <input type="text" v-model="title" required />
      <small class="danger">{{ message }}</small>
    </div>
    <div>
      <label>Detail</label>
      <input type="text" v-model="detail" required />
      <small v-if="message" class="danger">{{ message }}</small>
    </div>
    <div class="text-center">
      <button>Submit</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      detail: "",
      message: "",
    };
  },
  methods: {
    submit() {
      fetch("http://localhost:3000/projects", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          title: this.title,
          detail: this.detail,
          complete: false,
        }),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => {
          console.log(err.message());
        });
    },
  },
};
</script>

<style scoped>
form {
  margin: 30px auto;
  background-color: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
button {
  background-color: #42b983;
  color: white;
  padding: 10px 30px;
  border-radius: 10px;
  margin-top: 30px;
  cursor: pointer;
}
.text-center {
  text-align: center;
}
.danger {
  color: crimson;
}
</style>
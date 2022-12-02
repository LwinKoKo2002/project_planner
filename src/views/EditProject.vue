<template>
  <h1>Edit Project</h1>
  <form @submit.prevent="submit">
    <div>
      <label>Title</label>
      <input type="text" v-model="title" required />
    </div>
    <div>
      <label>Detail</label>
      <input type="text" v-model="detail" required />
    </div>
    <div class="text-center">
      <button>Update</button>
    </div>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      api: "http://localhost:3000/projects/",
      title: "",
      detail: "",
    };
  },
  methods: {
    submit() {
      fetch(this.api + this.id, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          title: this.title,
          detail: this.detail,
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
  mounted() {
    fetch(this.api + this.id)
      .then((res) => {
        return res.json();
      })
      .then((data) => {
        this.title = data.title;
        this.detail = data.detail;
      })
      .catch((err) => {
        console.log(err.message());
      });
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
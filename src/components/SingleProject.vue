<template>
  <div class="project">
    <div class="actions" @dblclick="toggleDetail">
      <h3>{{ project.title }}</h3>
      <div class="icons">
        <span class="material-icons edit">edit</span>
        <span class="material-icons delete" @click="deleteProject">delete</span>
        <span class="material-icons done">done</span>
      </div>
    </div>
    <div class="details" v-if="showDetails">
      <p>
        {{ project.details }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      uri: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    toggleDetail() {
      this.showDetails = !this.showDetails;
    },
    deleteProject() {
      fetch(this.uri, { method: "DELETE" })
        .then(() => this.$emit("deleteProject", this.project.id))
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
/* .material-icons:hover {
  color: #777;
} */
.edit:hover {
  color: #fb9300;
}
.delete:hover {
  color: #f54748;
}
.done:hover {
  color: #66de93;
}
.project:hover {
  background-color: #dbe6fd;
}
</style>

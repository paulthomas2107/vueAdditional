<template>
  <h1>Hello Paul</h1>
  <p>Your static HTML</p>
  <p v-once>
    My name is {{ name }} and I am from {{ channel }}, my age is {{ age }}
  </p>
  <p>RAW HTML {{ bitsOfHTML }}</p>
  <p v-html="bitsOfHTML"></p>
  <p>My languages : </p>
  <ul>
    <li v-bind:key="lang" v-for="lang in languages">{{ lang}}</li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      bitsOfHTML: "<b>I AM BOLD HTML</b>",
      languages: ["Java", "C++", "Vue", "React"],
      name: "Rory Thomas",
      channel: "Whatever Videos",
      age: 16,
    };
  },
  methods: {
    helloWorld() {
      //alert('Hello '+this.name);
    },
  },
  beforeCreate() {
    console.log(this.name);
    console.log("Before create....");
  },
  created() {
    console.log(this.name);
    console.log("Created....");
  },
  beforeMount() {
    console.log(this.name);
    console.log("Before mount....");
  },
  beforeUnmount() {
    console.log(this.name);
    console.log("Before unmount....");
  },
  unmounted() {
    console.log(this.name);
    console.log("Unmounted...");
  },
  mounted() {
    console.log(this.name);
    console.log("Mounted");
    this.name = "Differ";
    this.helloWorld();
  },
};
</script>

<style scoped>
h1 {
  color: red;
}
</style>

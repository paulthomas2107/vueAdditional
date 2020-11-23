<template>
  <div>
    <h1>Hello Paul</h1>
    <p>Your static HTML</p>
    <p v-once>
      My name is {{ name }} and I am from {{ channel }}, my age is {{ age }}
    </p>
    <p>RAW HTML {{ bitsOfHTML }}</p>
    <p v-html="bitsOfHTML"></p>
    <p>My languages :</p>
    <ul>
      <li v-for="(lang, index) in languages" v-bind:key="lang.name">
        {{ index + 1 }} {{ lang.name }} {{ lang.type }}
      </li>
    </ul>
    <p><b>Random</b></p>
    {{ randomItem }}
    <br />
    <br />
    <button @click="randomMethod">Generate Random</button>
    <br />
    <p>Number: {{ randomNumber }}</p>
    <input v-bind:value="randomNumber" @input="changeNumber($event)" />
    <button @click="randomMethod2">Generate Random</button>
    <br />
    <input v-model="randomNumber" />
    <br /><br />
    <p>{{ keywords.join(" | ") }}</p>
    <input :value="inputValue" @keyup.space="processInput($event)" />
  </div>

  <div>
    <h1>Speed Typer.</h1>
    <p>Your score is {{ keywords.filter(keyword => 
      keyword.correct).length}}</p>
    <p>
      <span
        :class="{
          correct: keyword.correct,
          wrong: keyword.wrong,
          pending: keyword.pending,
        }"
        :key="keyword.text"
        v-for="keyword in keywords"
        >{{ keyword.text }}&nbsp;</span
      >
    </p>
    <input
      type="text"
      :value="inputValue"
      @keyup.space="processSpeedInput($event)"
    />
  </div>
</template>

<script>
const defaultKeywords = [
  "template",
  "data",
  "javascript",
  "guilani",
  "Pense",
  "headache",
  "provident",
  "this",
  "drrastic",
  "plium",
  "github",
  "facebook",
  "jones",
  "hotdog",
  "perfection",
].map((keyword) => {
  return {
    text: keyword,
    correct: false,
    wrong: false,
    pending: true,
  };
});

export default {
  data() {
    return {
      inputValue: "",
      keywords: defaultKeywords,
      index: 0,

      randomNumber: Math.random(),
      randomItem: "0",
      bitsOfHTML: "<b>I AM BOLD HTML</b>",
      languages: [
        { name: "Java", type: "OO" },
        { name: "C++" },
        { name: "Vue" },
        { name: "React", type: "Generic" },
      ],
      name: "Rory Thomas",
      channel: "Whatever Videos",
      age: 16,
    };
  },
  methods: {
    processSpeedInput(event) {
      const value = event.target.value.trim();

      if (value === "") {
        return;
      }

      if (this.keywords[this.index].text === value) {
        this.keywords[this.index].correct = true;
        this.keywords[this.index].wrong = false;
        this.keywords[this.index].pending = false;
      } else {
        this.keywords[this.index].correct = false;
        this.keywords[this.index].wrong = true;
        this.keywords[this.index].pending = false;
      }
      this.inputValue = "";
      this.index++;
    },
    processInput(event) {
      const value = event.target.value;
      this.keywords[this.index] = value;
      this.inputValue = "";
      this.index++;
    },
    changeNumber(e) {
      this.randomNumber = e.target.value;
    },
    randomMethod() {
      this.randomItem = Math.random();
    },
    randomMethod2() {
      this.randomNumber = Math.random();
    },
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
button {
  color: red;
  background-color: chartreuse;
}
input {
  border-color: black;
}

div {
  border-style: groove;
  border-color: black;
}

.pending {
  font-weight: bold;
  text-decoration: underline;
}

.correct {
  font-weight: bold;
  color: green;
}

.wrong {
  font-weight: bold;
  color: red;
}
</style>

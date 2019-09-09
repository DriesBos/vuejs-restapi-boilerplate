<template>
  <div class="container">
    <div class="center-block">
      <input v-model="input" placeholder="input" type="text" />
      <button @click="submitQuery(input)">submit</button>
      <p>{{ info }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { key, proxy } from "~/plugins/config";

export default {
  data() {
    return {
      info: null,
      input: ""
    };
  },
  methods: {
    submitQuery: function(input) {
      if (input !== "") {
        axios
          .get(`${proxy}https://food2fork.com/api/search?key=${key}&q=${input}`)
          .then(response => (this.info = response))
          .catch(error => {
            console.log(error.response);
          });
      }
    }
  }
};
</script>

<style>
.container {
  position: relative;
  width: 100%;
  height: 100vh;
  background: #dedede;
}
.center-block {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
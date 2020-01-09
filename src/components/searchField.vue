<template>
  <v-row justify="end">
    <input
      type="text"
      id="myInput"
      v-on:keyup="textSearch()"
      v-model="textF"
      placeholder="Search.. (-(-(-.-)-)-)"
    />
  </v-row>
</template>
<script>
export default {
  name: "searchField",

  props: {},
  data: () => ({
    textF: ""
  }),
  methods: {
    textSearch: function() {
      this.$emit("inputTyped", this.textF.toUpperCase());
    }
  }
};
</script>
<style scoped>
#myInput {
  background-color: white;
  padding: 0.5vh 0.5vw 0.5vh 0.5vw;

  width: 20vw;
  font-size: 16px;
  text-align: start;
  border: 1px solid #ddd;
  margin-right: 5%;
  color: black;
}
</style>
<template>
  <div>
    <div class="flip-card">
      <div class="flip-card-inner">
        <div class="flip-card-front">
          <img v-bind:src="coverUrl" alt="Avatar" />
        </div>
        <div class="flip-card-back">
          <h3>{{bookTitle}}</h3>
          <p>{{bookDescription}}</p>
          <button
            v-bind:name="indexShelf"
            @click="onClick(indexShelf, true)"
            class="myButton"
          >More Information</button>
          <!--  = !overlay" -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "bookShelf",
  props: {
    coverUrl: String,
    bookTitle: String,
    bookDescription: String,
    indexShelf: Number
  },

  data: () => ({}),

  methods: {
    onClick: function(valueTrans, overlayDisp) {
      this.$emit("buttonFired", valueTrans, overlayDisp);
    }
  }
};
</script>
<style scoped>
.flip-card {
  background-color: transparent;
  width: 35vh;
  height: 50vh;
  margin: 20px 20px 20px 20px;
  perspective: 1000px;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front img {
  width: 100%;
  height: 100%;
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: auto;
  height: 54vh;
  backface-visibility: hidden;
}

.flip-card-front {
  background-color: #bbb;
  color: black;
}

.flip-card-back {
  background: #2980b9;
  background: -webkit-linear-gradient(to right, #2980b9, #2c3e50);
  background: linear-gradient(to right, #2980b9, #2c3e50);
  color: white;
  transform: rotateY(180deg);
}

.flip-card-back h3 {
  margin-top: 10%;
  font-size: 3.5vh;
}

.flip-card-back p {
  font-size: 1vw;
  margin-top: 8%;
  padding-left: 15px;
  padding-right: 15px;
}

.flip-card-back p {
  font-size: 2.5vh;
}

button {
  display: inline;
  background-color: #f8f9fa;
  /*  width: auto;
  height: 4vh; */
  color: black;
  font-family: oswald;
  position: fixed;
  font-size: 2vh;
  left: 50%;
  bottom: 1%;
  transform: translate(-50%, -50%);
  padding: 0.2vh 0.2vw 0.2vh 0.2vw;
  font-family: "Oswald", sans-serif;
  margin: 0 auto;
}

button:hover {
  background-color: lightgrey;
}
</style>
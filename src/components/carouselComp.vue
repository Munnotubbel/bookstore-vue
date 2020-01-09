  <template>
  <v-flex align-center>
    <v-row justify="center">
      <img v-bind:src="detailUrl" alt="Avatar" style="min-height:200px ;width:auto;height:20vw;" />
    </v-row>
    <v-row justify="center">
      <v-card class="mt-3 mb-3" style="min-width: 300px ;width:40vw;height:auto;" justify="center">
        <h3 class="carousel_h3">{{ carouselTitle}}</h3>

        <v-row justify="center">
          <p class="carousel_p">{{ carouselDescription }}</p>
        </v-row>
      </v-card>
    </v-row>
  </v-flex>
</template>
<script>
export default {
  name: "carouselComp",
  props: {
    detailUrl: String,
    carouselTitle: String,
    carouselDescription: String,
    indexCarousel: Number
  },
  data: () => ({})
};
</script>
<style scoped>
.carousel_h3 {
  font-size: 3vh;
  display: block;
  text-align: center;
  margin-top: 2vw;
  color: white;
}

.carousel_p {
  display: block;
  font-size: 2vh;

  margin-left: auto;
  margin-right: auto;
  padding: 3%;
  width: 70%;
  color: white;
}
</style>
<template>
  <v-app>
    <v-app-bar class fixed dense scroll-target="#scroll" style="background:#757575">
      <searchField v-on:inputTyped="filterMethod" />
    </v-app-bar>
    <v-content style="background:#757575">
      <v-container>
        <v-row justify="center" class="maintitle">{{pagetitle}}</v-row>
        <v-row justify="center" class="subtitle">{{pagesubtitle}}</v-row>
      </v-container>

      <v-card v-if="displayOverlay">
        <v-overlay :value="overlay">
          <v-row justify="center">
            <div class="carouselBackground">
              <v-carousel
                hide-delimiters
                width="800px"
                height="auto"
                v-model="model"
                justify="center"
              >
                <v-row justify="end ">
                  <v-btn class="carousel_Button" icon @click="onclickClose">Close</v-btn>
                </v-row>
                <v-carousel-item v-for="(carousel, index) in filterTitle" :key="index">
                  <carouselComp
                    :indexCarousel="index"
                    :detailUrl="carousel.detail"
                    :carouselTitle="carousel.title"
                    :carouselDescription="carousel.description"
                  />
                </v-carousel-item>
              </v-carousel>
            </div>
          </v-row>
        </v-overlay>
      </v-card>

      <div v-if="loading">loading</div>
      <section v-else id="bookshelf" class="d-flex flex-row flex-wrap justify-content-center">
        <div v-for="(booklet, index) in filterTitle" :key="index">
          <bookShelf
            v-on:buttonFired="moreInfoBtn"
            :indexShelf="index"
            :coverUrl="booklet.cover"
            :bookTitle="booklet.title"
            :bookDescription="booklet.description"
          />
        </div>
      </section>
    </v-content>
  </v-app>
</template>

<script>
import bookShelf from "./components/bookShelf";
import searchField from "./components/searchField";
import carouselComp from "./components/carouselComp";
export default {
  name: "App",
  components: {
    bookShelf,
    searchField,
    carouselComp
  },
  data: () => ({
    pagetitle: "Bookstore",
    pagesubtitle: "we have the finest selection",
    loading: true,
    displayOverlay: false,
    bookdata: {},
    buchDaten: [],
    model: 0,
    textSearch: ""
  }),
  created() {
    this.getBookData();
  },
  computed: {
    filterTitle: function() {
      return this.buchDaten.filter(booklet => {
        return booklet.title.toUpperCase().match(this.textSearch);
      });
    }
  },

  methods: {
    filterMethod(text) {
      this.textSearch = text;
    },
    moreInfoBtn(x, y) {
      this.model = x;
      this.displayOverlay = y;
    },

    onclickClose: function() {
      this.displayOverlay = false;
    },

    getBookData: async function() {
      const response = await fetch("https://api.myjson.com/bins/zyv02");

      var data = await response.json();

      this.buchDaten = data.books;
      this.loading = false;
    }
  }
};
</script>
<style>
@import url("https://fonts.googleapis.com/css?family=Abril+Fatface&display=swap");
@import url("https://fonts.googleapis.com/css?family=Roboto:300&display=swap");
@import url("https://fonts.googleapis.com/css?family=Oswald&display=swap");

#bookshelf {
  margin-left: auto;
  margin-right: auto;
}
.maintitle,
.subtitle {
  font-family: "Abril Fatface", cursive;
  color: white;
}
.maintitle {
  font-size: 7vw;
  margin-top: 1%;
}
.subtitle {
  font-size: 2vw;
  margin-top: -3vw;
}
body {
  font-family: "Roboto", sans-serif;
}

.carouselBackground {
  background: #2980b9;
  background: -webkit-linear-gradient(to right, #2980b9, #2c3e50);
  background: linear-gradient(to right, #2980b9, #2c3e50);
  color: white;
  width: 80%;
  height: auto;
}

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

.carousel_Button {
  background-color: darkgray;

  color: black;
  font-family: oswald;
  margin-top: 4%;
  margin-right: 4%;
  font-size: 2vh;

  transform: translate(-50%, -50%);

  font-family: "Oswald", sans-serif;
}
</style>
<template>
  <div class="home" id="home">
    <NavBar :st="this.filmes" :sz="this.allTV1" />
    <HelloWorld :st="filmes" />
    <ALLCOm />
    <BestMovies />
    <BestTV />
    <AsideMnue />
  </div>
</template>
<script>
// @ is an alis to /src
import { mystore } from "@/store/count";
import { mapState, mapActions } from "pinia";
import { ListsStore1 } from "../store/Lists";
import HelloWorld from "@/components/HelloWorld.vue";
import BestMovies from "@/components/BestMovies.vue";
import AsideMnue from "@/components/AsideMnue.vue";
import NavBar from "@/components/NavBar.vue";
import ALLCOm from "@/components/ALLCOm.vue";
import BestTV from "@/components/BestTV.vue";
export default {
  name: "HomeView",
  components: {
    HelloWorld,
    BestMovies,
    AsideMnue,
    BestTV,
    NavBar,
    ALLCOm,
  },
  data() {
    return {
      filmes: "",
    };
  },
  provide() {
    return {
      fun: this.doget,
      funtv: this.dogetTV,
      trialmovis: this.getTrialmovie,
    };
  },
  methods: {
    ...mapActions(ListsStore1, ["updateL"]),
    ...mapActions(mystore, [
      "dogetAll",
      "dogetAlltv",
      "dogetTV",
      "doget",
      "getTrialmovie",
      "ALLfun",
    ]),
    dop() {
      console.log("doneprovide");
    },
  },
  computed: {
    ...mapState(mystore, ["count", "allTV1", "singeltv", "trial", "ALL"]),
  },
  async mounted() {
    document.body.style.backgroundImage = 'url("../assets/1.jpg")';
    await this.dogetAlltv();
    await this.dogetAll();
    await this.ALLfun();
    await this.getTrialmovie();
    await this.updateL();
    this.filmes = this.count;
    await this.updateL();
  },
};
</script>

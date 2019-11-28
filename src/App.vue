<template>
  <div id="app">
    <p>Show sigmas</p>
    <input type="checkbox" v-model="sigma" />
    <p>Show vector arrows.</p>
    <input type="checkbox" v-model="vec" />
    <p>Show lables.</p>
    <input type="checkbox" v-model="lables" />
    <h1>List of data, formulae and relationships</h1>
    <h2>Mechanics</h2>
    <h3>Kinematic equations of motion</h3>
    <Mathr :formula="s_uvt" size="small" />
    <Mathr :formula="f_ma" size="small" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Mathr from "./components/Mathr.vue";
@Component({
  components: {
    Mathr
  },
  props: {
    sigma: Boolean,
    vec: Boolean,
    lables: Boolean
  },
  data() {
    return {
      msg: "Hello"
    };
  },
  methods: {}
})
export default class App extends Vue {
  sigma = false;
  vec = false;
  lables = false;
  get s_uvt(): string {
    return `${this.maybe_lables(
      this.maybe_vec("s"),
      "displacement"
    )}=\\frac{(${this.maybe_lables(
      this.maybe_vec("u"),
      "initial velocity"
    )}+${this.maybe_lables(
      this.maybe_vec("v"),
      "final velocity"
    )})${this.maybe_lables("t", "time")}}{2}`;
  }

  get f_ma(): string {
    return `${this.maybe_sigma(
      this.maybe_lables(this.maybe_vec("F"), "force")
    )}=${this.maybe_lables("m", "mass")}${this.maybe_lables(
      this.maybe_vec("a"),
      "acceleration"
    )}`;
  }

  maybe_lables = (s: string, l: string): string =>
    this.lables ? `${s}_{\\text{(${l})}}` : s;
  maybe_sigma = (s: string): string => (this.sigma ? `\\sum ${s}` : s);
  maybe_vec = (s: string): string => (this.vec ? `\\vec{${s}}` : s);
}
</script>

<style lang="sass">
#app
  font-family: Roboto, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px
</style>

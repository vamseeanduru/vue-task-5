<template>
<div class="conatiner">
  <h1 v-if="show">Planets</h1>
  <br />
  <button class="btn btn-outline-danger" v-if="show" @click="show = !show">
    +
  </button>
  <br />
  <router-link to="/"><button class="btn btn-success">Home</button></router-link>
  <table-view v-if="show" :externalTableData="planetsData"> </table-view>
  <planets-form v-if="!show" @addPlanetsToTable="showData"></planets-form>
</div>
</template>

<script>
import PlanetsForm from "./PlanetsForm.vue";
import TableView from "@/components/TableView.vue";

export default {
  components: {
    PlanetsForm,
    TableView,
  },
  name: "GetPlanets",
  data() {
    return {
      show: true,
    };
  },
  created() {},
  methods: {
    showData(data) {
      this.show = true;
      this.planetsData.push(data);
    },
  },
  computed: {
    planetsData() {
      return this.$store.state.planetsData
    }
  },
  mounted() {
    this.$store.dispatch("getPlanetsData")
  }
};
</script>

<style scoped>
.btn-success {
  margin-right: 95%;
  margin-bottom: 20px;
}

.btn-outline-danger {
  margin-right: 96%;
  margin-bottom: 20px;
}
</style>

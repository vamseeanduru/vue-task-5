<template>
<div class="conatiner">
  <h1 v-if="show">Characters</h1>
  <br />
  <button class="btn btn-outline-danger" v-if="show" @click="show = !show">
    +
  </button>
  <br />
  <router-link to="/"><button class="btn btn-success">Home</button></router-link>
  <table-view v-if="show" :externalTableData="charactersData">></table-view>
  <characters-form v-if="!show" @addCharactersToTable="showData"></characters-form>
</div>
</template>

<script>
import CharactersForm from "./CharactersForm.vue";
import TableView from "@/components/TableView.vue";
export default {
  components: {
    CharactersForm,
    TableView
  },
  name: "GetCharacters",
  data() {
    return {
      show: true,
    };
  },
  created() {},
  methods: {
    showData(data) {
      this.show = true;
      this.charactersData.push(data);
    },
  },
  computed: {
    charactersData() {
      return this.$store.state.charactersData
    }
  },
  mounted() {
    this.$store.dispatch("getCharactersData");
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

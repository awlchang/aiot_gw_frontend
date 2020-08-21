<template>
  <v-container fill-height fluid align-content-center>
    <v-row no-gutters flex-wrap:nowrap>
      <Performance class="mb-3" />
    </v-row>
    <v-row no-gutters flex-wrap:nowrap>
      <Table />
    </v-row>
  </v-container>
</template>

<script>
import Performance from "../components/scripts/Performance";
import Table from "../components/scripts/Table";

export default {
  components: {
    Table,
    Performance
  }
};
</script>

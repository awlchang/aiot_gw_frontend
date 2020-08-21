<template>
  <v-card class="mx-auto" max-width="95%" min-width="50%" outlined>
    <v-card-title>
      <v-icon large left>
        mdi-router-wireless
      </v-icon>
      <span class="title font-weight-light"
        >192.168.0.1
        <v-btn icon @click="callDevice()"><v-icon>mdi-bell</v-icon></v-btn>
      </span>
    </v-card-title>

    <v-subheader class="text-h6">System Performance:</v-subheader>
    <v-card-text class="headline text-center">
      All Good
    </v-card-text>

    <v-row no-gutters>
      <v-col v-for="item in items" :key="item.index">
        <v-list-item>
          <v-list-item-icon>
            <v-icon large :color="item.color">{{ item.icon }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title
              class="text-h6"
              v-text="item.title"
            ></v-list-item-title>
            <v-list-item-subtitle v-text="item.subtitle"></v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-col>
    </v-row>
  </v-card>
</template>

<style scoped>
.v-list-item__icon:first-child {
  margin-right: 10px;
  padding-left: 0px;
}
</style>

<script>
export default {
  data: () => ({
    items: [
      {
        title: "26",
        subtitle: "Temperature",
        icon: "mdi-thermometer",
        color: "light-blue"
      },
      {
        title: "60%",
        subtitle: "CPU Usage",
        icon: "mdi-cpu-64-bit",
        color: "green"
      },
      {
        title: "50%",
        subtitle: "Memory Usage",
        icon: "mdi-memory",
        color: "lime"
      },
      {
        title: "5.6G/16G",
        subtitle: "Storage Usage",
        icon: "mdi-database",
        color: "blue-grey"
      }
    ]
  }),
  methods: {
    callDevice() {
      alert("call");
    }
  }
};
</script>

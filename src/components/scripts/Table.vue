<template>
  <v-card class="mx-auto pa-5" max-width="100%" min-width="50%" outlined>
    <v-card-title>
      <v-chip
        close
        color="primary"
        text-color="white"
        close-icon="mdi-logout"
        @click:close="logout"
      >
        <v-avatar left>
          <v-icon>mdi-account-circle</v-icon>
        </v-avatar>
        Ranee's Script
      </v-chip>
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>

    <v-data-table
      :headers="headers"
      :items="infos"
      :search="search"
      @click:row="showDetails"
    >
      <template v-slot:item.name="{ item }">
        <v-badge bordered color="error" dot v-model="item.dot">
          {{ item.name }}
        </v-badge>
      </template>
      <template v-slot:item.device="{ item }">
        <v-btn text small @click.stop="device()">
          {{ item.device }}
        </v-btn>
      </template>
      <template v-slot:item.action="{ item }">
        <v-btn icon color="green">
          <v-icon color="green darken-1" @click.stop="runScript(item)">
            {{ item.actionIcon }}
          </v-icon>
        </v-btn>
      </template>

      <template v-slot:top>
        <v-dialog v-model="dialog" max-width="500px">
          <v-card>
            <v-card-title class="headline grey lighten-2">
              <span>{{ scriptDetails.name }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="scriptDetails.date"
                      label="Last Updated"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="scriptDetails.name"
                      label="Name"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="close">CLOSE</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
import { eventBus } from "../../main";

export default {
  data: () => ({
    dialog: false,
    search: "",
    headers: [
      { text: "Last updated", align: "start", value: "date" },
      { text: "Name", value: "name" },
      { text: "Devices", value: "device", sortable: false },
      { text: "Action", value: "action", filterable: false, sortable: false }
    ],
    scripts: [],
    scriptIndex: -1,
    scriptDetails: {
      data: "",
      name: ""
    },
    defaultDetails: {
      data: "",
      name: ""
    },
    computed: {
      formTitle() {
        return this.scriptIndex === -1 ? "New Item" : "Edit Item";
      }
    },
    watch: {
      dialog(val) {
        val || this.close();
      }
    },
    infos: [
      {
        date: "2020/05/01 00:00:00",
        name: "Dou Dou's house",
        dot: false,
        device: "Select Devices",
        actionIcon: "mdi-play"
      },
      {
        date: "2018/10/12 00:00:00",
        name: "storytelling",
        dot: false,
        device: "Select Devices",
        actionIcon: "mdi-play"
      },
      {
        date: "2020/01/01 00:00:00",
        name: "farmer game",
        dot: false,
        device: "Select Devices",
        actionIcon: "mdi-play"
      },
      {
        date: "2021/02/01 00:00:00",
        name: "Classfier",
        dot: false,
        device: "Select Devices",
        actionIcon: "mdi-play"
      }
    ]
  }),
  methods: {
    runScript(item) {
      item.dot = item.dot == false ? true : false;
      item.actionIcon = item.actionIcon == "mdi-play" ? "mdi-stop" : "mdi-play";
      // alert("Alert! \n" + item.date);
    },
    showDeviceDrawer() {
      eventBus.$emit("showDeviceDrawer", true);
    },
    showDetails(data) {
      this.scriptIndex = this.scripts.indexOf(data);
      this.scriptDetails = Object.assign({}, data);
      this.dialog = true;
    },
    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.scriptDetails = Object.assign({}, this.defaultItem);
        this.scriptIndex = -1;
      });
    },
    logout() {
      this.$router.push("/");
    },
    device() {
      // alert("Alert! \n");
      this.$router.push("/devices");
    }
  }
};
</script>

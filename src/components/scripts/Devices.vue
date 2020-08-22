<template>
  <v-container fill-height fluid>
    <v-card class="mx-auto px-3" elevation="0" max-width="100%" min-width="30%">
      <v-row align="center" justify="center">
        <v-col class="d-flex" cols="auto">
          <v-select
            v-model="model"
            class="text-h6"
            :items="scriptName"
            :menu-props="{ bottom: true, offsetY: true }"
            @input="setSelected"
          ></v-select>
        </v-col>
      </v-row>
      <template v-for="item in items">
        <v-row :key="item.index" justify="start">
          <v-list-item>
            <v-list-item-icon>
              <v-icon class="pl-3">{{ item.action }}</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
              <v-list-item-subtitle>usage rate: 6/12</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-row>

        <v-slide-group multiple :key="item.index" class="pb-5">
          <v-slide-item v-for="subitem in item.items" :key="subitem.index">
            <v-card
              class="max-auto mx-1"
              max-height="100%"
              width="165"
              :color="subitem.vacant_color"
              outlined
            >
              <v-card-actions class="py-0">
                <v-list-item>
                  <v-row align="start" justify="space-between">
                    <v-icon @click="addDevice(subitem)">{{
                      subitem.add_device_icon
                    }}</v-icon>
                    <div v-show="subitem.vacant_color == ''">Vacant</div>
                    <v-icon @click="callDevice()">{{ subitem.icon }}</v-icon>
                  </v-row>
                </v-list-item>
              </v-card-actions>
              <v-card-text
                class="text-md-body-1 text-center py-0 px-2 font-weight-medium"
              >
                <div class="span_script_name grey--text text--darken-3">
                  {{ subitem.run_script }}
                </div>
              </v-card-text>
            </v-card>
          </v-slide-item>
        </v-slide-group>
      </template>
    </v-card>
  </v-container>
</template>

<style>
.v-select__selections input {
  display: none;
}
.v-text-field .v-select__slot .v-select__selection--comma {
  min-width: min-content;
}

/* 腳本選擇的style */
.v-select__selection {
  line-height: 25px;
}
.mdi-menu-down {
  margin-top: 5px;
}

.v-application--is-ltr .v-list-item__icon:first-child {
  margin-right: 20px;
}

.span_script_name {
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}
.span_script_name:hover {
  -webkit-line-clamp: initial;
}
</style>

<script>
export default {
  data: () => ({
    scriptName: ["Classfiergg", "farmer game", "storytelling", "Dou Dou's house"],
    model: "",
    selected_value: "",
    items: [
      {
        action: "mdi-robot",
        title: "Robots",
        items: [
          {
            title: "robot",
            ip: "192.168.0.2",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          },
          {
            title: "tablet",
            ip: "192.168.0.4",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          },
          {
            title: "tablet",
            ip: "192.168.0.5",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          }
        ]
      },
      {
        action: "mdi-tablet",
        title: "Tablets",
        active: false,
        items: [
          {
            title: "tablet",
            ip: "192.168.0.3",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          },
          {
            title: "tablet",
            ip: "192.168.0.11",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          },
          {
            title: "tablet",
            ip: "192.168.0.12",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          },
          {
            title: "tablet",
            ip: "192.168.0.13",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          },
          {
            title: "tablet",
            ip: "192.168.0.14",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          }
        ]
      },
      {
        action: "mdi-toy-brick",
        title: "Toys",
        active: false,
        items: [
          {
            title: "Toy",
            ip: "192.168.0.6",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          },
          {
            title: "Toy",
            ip: "192.168.0.7",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          }
        ]
      },
      {
        action: "mdi-radar",
        title: "Sensors",
        active: false,
        items: [
          {
            title: "Touch",
            ip: "192.168.0.8",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          },
          {
            title: "Temperature",
            ip: "192.168.0.15",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          },
          {
            title: "NFC Reader",
            ip: "192.168.0.16",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          },
          {
            title: "tablet",
            ip: "192.168.0.17",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          },
          {
            title: "tablet",
            ip: "192.168.0.18",
            datetime: "2020/12/12 00:00:00",
            add_device_icon: "mdi-puzzle-plus",
            icon: "mdi-bell",
            vacant_color: "",
            run_script: ""
          }
        ]
      }
    ]
  }),
  created: function() {
    this.model = this.scriptName[0];
    this.selected_value = this.scriptName[0];
  },
  methods: {
    addDevice(item) {
      item.add_device_icon =
        item.add_device_icon == "mdi-puzzle-plus"
          ? "mdi-puzzle-minus"
          : "mdi-puzzle-plus";

      item.vacant_color = item.vacant_color == "" ? "brown lighten-4" : "";
      item.run_script = item.run_script == "" ? this.selected_value : "";
    },
    callDevice() {
      alert("call");
    },
    setSelected(value) {
      this.selected_value = value;
      // this.model = value;
    }
  }
};
</script>

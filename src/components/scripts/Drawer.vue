<template>
  <v-navigation-drawer v-model="isShowDrawer" app overflow>
    <v-list nav>
      <v-subheader>Devices</v-subheader>
      <v-list-group
        v-for="item in items"
        :key="item.title"
        v-model="item.active"
        :prepend-icon="item.action"
        no-action
        sub-group
      >
        <template v-slot:activator>
          <v-list-item-content>
            <v-list-item-title v-text="item.title">{{item.title}}</v-list-item-title>
          </v-list-item-content>
        </template>

        <template v-for="subItem in item.items">
          <v-list-item
            class="headline pl-8"
            two-line
            :key="subItem.title"
            @click="selected.push(subItem)"
          >
            <v-list-item-content>
              <v-list-item-title v-text="subItem.ip"></v-list-item-title>
              <v-list-item-subtitle
                v-text="subItem.datetime"
              ></v-list-item-subtitle>
            </v-list-item-content>
            <v-list-item-action>
              <v-icon v-text="subItem.icon" @click="aaa"></v-icon>
            </v-list-item-action>
          </v-list-item>
        </template>
        <v-divider></v-divider>
      </v-list-group>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
import { eventBus } from "../../main";

export default {
  created() {
    eventBus.$on("showDeviceDrawer", message => {
      this.isShowDrawer = message;
    });
  },
  data: () => ({
    selected: [],
    search: "",
    drawers: ["Default (no property)"],
    isShowDrawer: false,
    watch: {
      isShowDrawer(val) {
        val || this.close();
      }
    },
    items: [
      {
        action: "mdi-robot",
        title: "Robots",
        items: [
          {
            title: "robot",
            ip: "192.168.0.2",
            datetime: "2020/12/12 00:00:00",
            icon: "mdi-bell"
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
            icon: "mdi-bell"
          },
          {
            title: "tablet",
            ip: "192.168.0.4",
            datetime: "2020/12/12 00:00:00",
            icon: "mdi-bell"
          },
          {
            title: "tablet",
            ip: "192.168.0.5",
            datetime: "2020/12/12 00:00:00",
            icon: "mdi-bell"
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
            icon: "mdi-bell"
          },
          {
            title: "Toy",
            ip: "192.168.0.7",
            datetime: "2020/12/12 00:00:00",
            icon: "mdi-bell"
          },
          {
            title: "Toy",
            ip: "192.168.0.8",
            datetime: "2020/12/12 00:00:00",
            icon: "mdi-bell"
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
            icon: "mdi-bell"
          },
          {
            title: "Temperature",
            ip: "192.168.0.8",
            datetime: "2020/12/12 00:00:00",
            icon: "mdi-bell"
          },
          {
            title: "NFC Reader",
            ip: "192.168.0.8",
            datetime: "2020/12/12 00:00:00",
            icon: "mdi-bell"
          }
        ]
      }
    ],
    primaryDrawer: {
      model: true,
      type: "default (no property)"
    }
  }),
  computed: {
    allSelected() {
      return this.selected.length === this.items.length;
    },
    categories() {
      const search = this.search.toLowerCase();

      if (!search) return this.items[0].items;

      return this.items.filter(item => {
        const title = item.title.toLowerCase();

        return title.indexOf(search) > -1;
      });
    },
    selections() {
      const selections = [];

      for (const selection of this.selected) {
        selections.push(selection);
      }

      return selections;
    }
  },
  methods: {
    close() {
      this.isShowDrawer = false;
    },
    aaa() {}
  }
};
</script>

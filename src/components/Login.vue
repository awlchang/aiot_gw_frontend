<template>
  <v-container fill-height>
    <v-row>
      <v-col>
        <v-card class="mx-auto pa-5" max-width="30%" min-width="450" outlined>
          <v-row align="center" justify="center">
            <v-img
              class="ma-2"
              max-width="100"
              src="../assets/logo.svg"
            ></v-img>
          </v-row>
          <v-card-title class="headline mb-1 justify-center"
            >AIoT Gateway</v-card-title
          >
          <v-card-text>
            <v-form>
              <v-select
                :items="items"
                label="Account"
                prepend-icon="mdi-account"
              ></v-select>

              <v-text-field
                id="password"
                label="Password"
                name="password"
                prepend-icon="mdi-lock"
                :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
                :type="show ? 'text' : 'password'"
                @click:append="show = !show"
                :rules="[rules.required]"
              ></v-text-field>
              <v-btn block color="success" class="mt-10" @click="comfirm">
                comfirm
              </v-btn>
            </v-form>
          </v-card-text>
        </v-card>
        <v-footer color="transparent" class="mx-auto" padless width="450">
          <v-select :items="items" label="Languages"></v-select>
          <v-btn text color="grey darken-1">Privacy</v-btn>
          <v-btn text color="grey darken-1">Terms</v-btn>
        </v-footer>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      show: false,
      rules: {
        required: value => !!value || "Required."
      }
    };
  },
  methods: {
    comfirm() {
      this.$router.push("/script");
      //傳遞的引數用{{ $route.query.goodsId }}獲取
      // this.$router.push({path: '/cart?goodsId=12'})
    }
  }
};
</script>

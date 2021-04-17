<template>
  <v-row justify="center">
    <v-col cols="12" xl="10" lg="10" md="10" sm="4" height="900">
      <v-card class="mx-10 mt-5 px-5" dark style="border: 3px solid #e2c12c">
        <div>
          <br />
          <form>
            <v-row>
              <v-col cols="12" lg="12" xs="4">
                <v-text-field
                  v-model="form.wallet"
                  class="mx-4"
                  label="نام کیف پول خود را وارد نمایید*"
                  outlined
                  dense
                  color="#e2c12c"
                ></v-text-field>

                <v-select
                  v-model="form.crypto"
                  class="mx-4 d-block inputValide"
                  color="#e2c12c"
                  dense
                  label="لطفارمز ارز خود را وارد نمایید*"
                  outlined
                ></v-select>
                <div class="InputAddress">
                  <v-text-field
                    style="width: 80%"
                    v-model="form.address"
                    class="mt-4 mr-5 d-inline-block"
                    dense
                    outlined
                    color="#e2c12c"
                    label="آدرس خود را وارد نمایید*"
                    prepend-inner-icon="mdi-link"
                  ></v-text-field>
                  <v-icon color="green" class="mx-2 hidden-xs-only"
                    >mdi-shield-check</v-icon
                  >
                </div>
              </v-col>
            </v-row>
          </form>
          <v-col cols="12" md="6" xs="4">
            <v-switch
              class="mx-4 d-inline-block col-xs-2 text-nowrap"
              label="قابل مشاهده در انتخاب آدرس"
              color="success"
              value="success"
              hide-details
            ></v-switch>
            <v-btn color="green" class="mx-5" width="100" justify="center"
              >ذخیره</v-btn
            >
          </v-col>
        </div>

        <template>
          <v-toolbar
            dense
            flat
            dark
            class="mt-4"
            style="
              border: 0;
              border-top: 1px solid white;
              border-bottom: 1px solid white;
            "
          >
            <span>
              <v-btn flat color="red" size="30" @click="isHidden = !isHidden">
                <v-icon>mdi-text-search</v-icon></v-btn
              >
            </span>

            <span class="mr-5 hidden-xs-only">
              <v-btn flat color="green" size="30"
                ><v-icon>mdi-format-list-checks</v-icon></v-btn
              >
            </span>
            <v-text-field
              outlined
              dense
              class="col-5 col-xs-4 bg-secondary mt-6 mx-2"
              style="border-radius: 22px"
              color="#e2c12c"
              prepend-inner-icon="mdi-magnify"
              placeholder="جستجو..."
              v-if="!isHidden"
              v-model="filterText"
            ></v-text-field>
          </v-toolbar>
        </template>

        <!-- Table!-->
        <v-col col="12" lg="12" md="12" xs="8">
          <v-simple-table dark height="250" fixed-header>
            <template v-slot:default>
              <thead flat dense>
                <tr>
                  <th
                    style="
                      border: 0;
                      border-bottom: 2px solid #e2c12c;
                      font-size: 16px;
                    "
                  >
                    نام
                  </th>
                  <th
                    style="
                      border: 0;
                      border-bottom: 2px solid #e2c12c;
                      font-size: 16px;
                    "
                  >
                    نماد
                  </th>
                  <th
                    style="
                      border: 0;
                      border-bottom: 2px solid #e2c12c;
                      font-size: 16px;
                    "
                  >
                    رمز ارز
                  </th>
                  <th
                    style="
                      border: 0;
                      border-bottom: 2px solid #e2c12c;
                      font-size: 16px;
                    "
                  >
                    آدرس
                  </th>
                  <th
                    style="
                      border: 0;
                      border-bottom: 2px solid #e2c12c;
                      font-size: 16px;
                    "
                    class="text-center"
                  >
                    عملیات
                  </th>
                </tr>
              </thead>
              <tbody dark>
                <tr v-for="item in items" :key="item" class="justify-center">
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ item.name }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <cryptoicon :symbol="item.sign" size="35" />
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ item.sign }}
                  </td>

                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <v-icon color="#CDBB1E">mdi-close-outline</v-icon>

                    {{ item.address }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <v-col
                      cols="12"
                      xs="6"
                      class="d-flex justify-center align-center"
                    >
                      <v-btn
                        color="#C0392B"
                        class="mr-4 float-left"
                        @click="DeleteRow"
                        >حذف</v-btn
                      >
                    </v-col>
                  </td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>

          <div class="text-center col-md-12 col-lg-12">
            <v-pagination
              class="mt-4 justify-center"
              v-model="page"
              :length="4"
              prev-icon="mdi-menu-left"
              next-icon="mdi-menu-right"
            ></v-pagination>
          </div>
        </v-col>
        <!-- Table!-->
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data: () => ({
    form: {
      wallet: "",
      address: "",
      crypto: "",
    },
    items: [],
    page: 1,
    index: "",
    Clicked: true,
    isHidden: true,
    filterText: "",
  }),
  methods: {
    DeleteRow(item) {
      this.items.splice(item);
    },
  },

  mounted() {
    const config = {
      headers: {
        Authorization: `Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczpcL1wvY29yZS11LnNpZ21hZGV2b3BzLmlyXC9hcGlcL3VzZXJcL2xvZ2luIiwiaWF0IjoxNjE4NjM5MTM1LCJleHAiOjE2MTg2NjA3MzUsIm5iZiI6MTYxODYzOTEzNSwianRpIjoidGY2aHhSM1dhcUV1dW1mZiIsInN1YiI6NDE4NiwicHJ2IjoiODdlMGFmMWVmOWZkMTU4MTJmZGVjOTcxNTNhMTRlMGIwNDc1NDZhYSJ9.XH8QiOJhkRE4Tzua1JdZlpHLpKsu9skLtgP0wrHZhI4`,
      },
    };
    this.$axios
      .$get("/testapi/wallet/favorite?currency=btc", config)
      .then((response) => {
        this.items = response;
        console.log(response);
      })
      .catch((err) => {
        console.log(err);
      });
  },
  computed: {
    filteredFav() {
      return this.items.filter((element) => {
        return element.match(this.filterText);
      });
    },
  },
};
</script>

<style scoped>
</style>

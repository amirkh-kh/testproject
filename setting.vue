<template>
  <v-row justify="center">
    <v-col cols="12" xl="10" lg="10" md="4" sm="4" height="900">
      <v-card class="mx-10 mt-5 px-5" dark style="border: 3px solid #e2c12c">
        <div>
          <br />

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
                class="mx-4 d-block"
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

          <v-col cols="12" md="6" xs="4">
            <v-switch
              class="mx-4 d-inline-block"
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

        <template slot:activator="{ on, attrs }">
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
              <v-btn
                flat
                color="red"
                size="30"
                flat
                @click="isHidden = !isHidden"
                v-bind="attrs"
                v-on="on"
              >
                <v-icon>mdi-text-search</v-icon></v-btn
              >
            </span>

            <span class="mr-5">
              <v-btn flat color="green" size="30"
                ><v-icon>mdi-format-list-checks</v-icon></v-btn
              >
            </span>
            <v-text-field
              transition="fab-transition"
              outlined
              dense
              color="#e2c12c"
              style="margin-top: 24px; float: right; padding-right: 220px"
              prepend-inner-icon="mdi-magnify"
              placeholder="جستجو..."
              v-if="!isHidden"
            ></v-text-field>
          </v-toolbar>
        </template>

        <!-- Table!-->
        <v-col col="12" lg="12" md="8" xs="8">
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
                    ردیف
                  </th>
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
              <tbody v-if="List" dark>
                <tr v-for="(item, index) in Object.keys(List)" :key="item">
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ List[item].balance }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ List[item].persian_name }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <cryptoicon :symbol="item" size="35" />
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ List[item].balance_irt }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <v-icon color="#CDBB1E">mdi-close-outline</v-icon>
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <v-col
                      cols="12"
                      xs="6"
                      class="d-flex justify-center align-center"
                    >
                      <v-btn color="#C0392B" class="mr-4 float-left">حذف</v-btn>
                    </v-col>
                  </td>
                </tr>
              </tbody>

              <tbody v-if="List" dark>
                <tr v-for="(item, index) in Object.keys(List)" :key="item">
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ List[item].balance }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ List[item].persian_name }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <cryptoicon :symbol="item" size="35" />
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ List[item].balance_irt }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <v-icon color="#CDBB1E">mdi-close-outline</v-icon>
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <v-col
                      cols="12"
                      xs="6"
                      class="d-flex justify-center align-center"
                    >
                      <v-btn color="#C0392B" class="mr-4 float-left">حذف</v-btn>
                    </v-col>
                  </td>
                </tr>
              </tbody>

              <tbody v-if="List" dark>
                <tr v-for="(item, index) in Object.keys(List)" :key="item">
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ List[item].balance }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ List[item].persian_name }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <cryptoicon :symbol="item" size="35" />
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ List[item].balance_irt }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <v-icon color="#CDBB1E">mdi-close-outline</v-icon>
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <v-col
                      cols="12"
                      xs="6"
                      class="d-flex justify-center align-center"
                    >
                      <v-btn color="#C0392B" class="mr-4 float-left">حذف</v-btn>
                    </v-col>
                  </td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>

          <div class="text-center">
            <v-pagination
              class="mt-4"
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
import axios from "axios";

export default {
  data: () => ({
    form: {
      wallet: null,
      address: null,
      crypto: null,
    },
    List: null,
    page: 1,
    close: true,
    Clicked: true,
    isHidden: true,
  }),
  methods: {},

  mounted() {
    const config = {
      headers: {
        Authorization: `Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczpcL1wvY29yZS11LnNpZ21hZGV2b3BzLmlyXC9hcGlcL3VzZXJcL2xvZ2luIiwiaWF0IjoxNjE4MzgyMjYxLCJleHAiOjE2MTg0MDM4NjEsIm5iZiI6MTYxODM4MjI2MSwianRpIjoiMkx1TEJoekJVSFZRYll1eCIsInN1YiI6NDE4NiwicHJ2IjoiODdlMGFmMWVmOWZkMTU4MTJmZGVjOTcxNTNhMTRlMGIwNDc1NDZhYSJ9.MXi8hsq6XFZaGfKQM9mpoujO4jASAcNhM2V-6So5x5g`,
      },
    };
    axios
      .get("/testapi/wallet/get_all", config)
      .then((response) => {
        this.List = response.data;
        console.log(response);
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>

<style scoped>
</style>

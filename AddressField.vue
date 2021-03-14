<template>
  <v-row justify="center">
    <v-col cols="12" lg="6" md="4" sm="4" height="900">
      <v-card class="mx-10 mt-5 px-5" dark>
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
              ></v-text-field>

              <v-select
                v-model="form.crypto"
                class="mx-4 d-block"
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
            <v-btn color="green" width="100" @click="validate">ذخیره</v-btn>
          </v-col>
        </div>

        <v-toolbar
          dense
          flat
          class="mt-4 bg-dark"
          style="
            border: 0;
            border-top: 1px solid white;
            border-bottom: 1px solid white;
          "
        >
          <span>
            <v-icon color="red" size="30" flat>mdi-text-search</v-icon>
          </span>

          <span class="mr-5">
            <v-icon color="green" size="30" flat>mdi-format-list-checks</v-icon>
          </span>
        </v-toolbar>

        <!-- Table!-->
        <v-col col="12" lg="12" md="8" xs="8">
          <v-simple-table dark height="250">
            <template v-slot:default>
              <thead dark flat dense>
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
                    class="text-left"
                  >
                    عملیات
                  </th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="item in ListItem" :key="item">
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ item.row }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ item.name }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <v-icon color="#E8690C" size="35">{{ item.icon }}</v-icon>
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ item.bit }}
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    {{ form.address }}
                    <v-icon color="#CDBB1E">mdi-close-outline</v-icon>
                  </td>
                  <td dense style="border: 0; border-bottom: 1px solid white">
                    <v-col
                      cols="12"
                      xs="6"
                      class="d-flex justify-center align-center"
                    >
                      <v-btn
                        color="#5D561C"
                        class="d-inline-block float-left mr-3 flex-nowrap"
                        >ویرایش</v-btn
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
export default {
  data: () => ({
    form: {
      wallet: null,
      address: null,
      crypto: null,
    },
    page: 1,
    close: true,
    ListItem: [
      {
        row: "1",
        name: "آدرس خودم",
        icon: "mdi-bitcoin",
        bit: "بیت کوین BTC",
        Address: "",
      },
      {
        row: "2",
        name: "آدرس خودم",
        icon: "mdi-bitcoin",
        bit: "بیت کوین BTC",
        Address: "",
      },
      {
        row: "3",
        name: "آدرس خودم",
        icon: "mdi-ethereum",
        bit: " اتریوم ETC",
        Address: "",
      },
      {
        row: "4",
        name: "آدرس خودم",
        icon: "mdi-ethereum",
        bit: "اتریوم ETC",
        Address: "",
      },
    ],
  }),
};
</script>

<style scoped>
</style>

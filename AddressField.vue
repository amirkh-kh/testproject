<template>
  <v-row justify="center">
    <v-col cols="12" lg="6" md="4" sm="4" height="900">
      <v-card class="mx-10 mt-5 px-5" dark>
        <div>
          <br />
          <v-text-field
            v-model="form.wallet"
            class="mx-4"
            label="*نام کیف پول خود را وارد نمایید*"
            outlined
            dense
          ></v-text-field>

          <v-select
            v-model="form.address"
            class="mx-4"
            dense
            label="لطفارمز ارز خود را وارد نمایید*"
            outlined
          ></v-select>
          <v-row>
            <v-col cols="12" lg="9" sm="6">
              <v-text-field
                style="width: 80%"
                v-model="form.crypto"
                class="d-inline-flex mr-4 mt-3"
                dense
                outlined
                label="آدرس خود را وارد نمایید*"
                prepend-inner-icon="mdi-map-marker"
                requiered
              ></v-text-field>
            </v-col>
            <v-col>
              <v-icon color="green" class="mt-5">mdi-shield-check</v-icon>
            </v-col>
          </v-row>

          <v-row>
            <v-col cols="12" lg="6" sm="8">
              <v-switch
                v-model="message"
                class="mx-4"
                label="قابل مشاهده در انتخاب آدرس"
                color="success"
                value="success"
                hide-details
              ></v-switch>
            </v-col>
            <v-col lg="6" sm="4">
              <v-btn color="green" class="mt-3" @click="validate">ذخیره</v-btn>
            </v-col>
          </v-row>
        </div>

        <v-toolbar
          dense
          flat
          class="mt-4"
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
        <v-simple-table dark style="height: 200px">
          <template v-slot:default>
            <thead dark flat dense>
              <tr>
                <th>ردیف</th>
                <th>نام</th>
                <th>نماد</th>
                <th>رمز ارز</th>
                <th>عملیات</th>
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
                  <v-icon style="color: gold">{{ item.icon }}</v-icon>
                </td>
                <td dense style="border: 0; border-bottom: 1px solid white">
                  {{ item.bit }}
                </td>
                <td dense style="border: 0; border-bottom: 1px solid white">
                  <v-row cols="5">
                    <v-col lg="3"><v-btn color="warning">ویرایش</v-btn></v-col>
                    <v-col lg="2"><v-btn color="red">حذف</v-btn></v-col>
                  </v-row>
                </td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>

        <div class="text-center mt-13">
          <v-pagination
            style="margin-right: 0"
            v-model="page"
            :length="4"
            prev-icon="mdi-menu-left"
            next-icon="mdi-menu-right"
          ></v-pagination>
        </div>
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
      },
      {
        row: "2",
        name: "آدرس خودم",
        icon: "mdi-bitcoin",
        bit: "بیت کوین BTC",
      },
      {
        row: "3",
        name: "آدرس خودم",
        icon: "mdi-ethereum",
        bit: " اتریوم ETC",
      },
      {
        row: "4",
        name: "آدرس خودم",
        icon: "mdi-ethereum",
        bit: "اتریوم ETC",
      },
    ],
  }),
};
</script>

<style scoped>
</style>
<!-- ethereum -->
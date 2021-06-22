<template>
  <div class="d-flex align-center View">
    <v-row dir="rtl">
      <v-col cols="2" lg="2" sm="4">
        <v-card width="300" style="background: #fff; border-radius: 5px 5px 0 0">
          <!-- <div
            style="
              background: #4a6073;
              font: size 1.5rem;
              padding-left: 45px;
              border-radius: 5px 5px 0 0;
            "
          >
            <v-card-title></v-card-title>
          </div> -->
          <v-list flat>
            <v-subheader class="Headtxt">لیست رمز ارزها</v-subheader>
            <v-list-item-group v-model="selectedItem" color="primary">
              <v-list-item v-for="(name, id) in markets" :key="id">
                <v-list-item-icon>
                  <cryptoicon :symbol="name.base_sign"></cryptoicon>
                  <cryptoicon :symbol="name.currency_sign"></cryptoicon>
                </v-list-item-icon>
                <v-list-item-content>
                  <v-list-item-title
                    ><v-text class="mx-3">
                      {{ name.base_persian }}-{{ name.currency_persian }}
                    </v-text></v-list-item-title
                  >
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-card>
      </v-col>

      <!-- orderbook -->
      <v-col cols="5">
        <v-card cols="12" width="400">
          <v-simple-table dense>
            <template v-slot:default>
              <thead class="txt" style="background: #02c076; border-radius: 5px 5px 0 0">
                <tr>
                  <th>قیمت</th>
                  <th>حجم</th>
                </tr>
              </thead>
              <tbody class="txt" style="background: #fff">
                <tr v-for="(item, id) in orderbook.buy" :key="id">
                  <td>{{ item.price }}</td>
                  <td>{{ item.amount }}</td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>

          <v-simple-table dense>
            <template v-slot:default>
              <thead style="background: #ff5252; border-radius: 5px 5px 0 0" class="txt">
                <tr>
                  <th>قیمت</th>
                  <th>حجم</th>
                </tr>
              </thead>

              <tbody class="txt" style="background: #fff">
                <tr v-for="(item, id) in orderbook.sell" :key="id">
                  <td>{{ item.price }}</td>
                  <td>{{ item.amount }}</td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
        </v-card>
      </v-col>
      <v-col cols="5"></v-col>
    </v-row>
  </div>
</template>

<script>
// import Market from "../../rabin-orderbook/src/components/Market.vue";
import axios from "axios";
export default {
  data: () => ({
    socket: null,
    orderbook: null,
    markets: null,
    selectedItem: 1,
  }),
  methods: {
    startWebsocket() {
      this.socket = new WebSocket(`wss://core.rcazone.com/order/live/btc_irt`);
      this.socket.onmessage = (e) => {
        const newData = JSON.parse(e.data);
        // this.$store.commit("order/UPDATE_ORDER_BOOK", newData.data);
        this.orderbook = newData.data;
      };
    },
    getMarket() {
      return axios
        .get("http://core.rcazone.com/markets")
        .then((data) => {
          console.log(data);
          this.markets = data.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },

    putComma(number) {
      const parts = number.toString().split(".");
      parts[0] = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      return parts.join(".");
    },
  },
  mounted() {
    this.startWebsocket();
    this.getMarket();
  },
  destroyed() {
    if (this.socket) {
      this.socket.close();
      this.socket = null;
    }
  },
};
</script>
<style scoped>
.txt {
  text-align: center;
}
.View {
  align-items: center;
  background: rgb(0 0 0 / 20%);
}
.Headtxt {
  margin: 0;
  color: #fff;
  background: #4a6073;
  font-size: 20px;
}
</style>

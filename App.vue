<template>
  <div class="d-flex align-center View" style="height: 100vh">
    <v-row dir="rtl">
      <v-col cols="2">
        <v-card
          height="770"
          width="300"
          style="background: #fff; border-radius: 5px 5px 0 0"
        >
          <div
            style="
              background: #4a6073;
              font: size 1.5rem;
              padding-left: 45px;
              border-radius: 5px 5px 0 0;
            "
          >
            <v-card-title class="Headtxt px-4">لیست رمز ارزها</v-card-title>
          </div>
          <v-btn class="col-12" text v-for="(name, id) in markets" :key="id">
            <v-text class="text-right"
              >{{ name.base_persian }}-{{ name.currency_persian }}</v-text
            > </v-btn
          ><br />
        </v-card>
      </v-col>
      <v-col cols="5">
        <v-card
          cols="12"
          height="600"
          width="400"
          class="rounded-lg"
          justify="center"
        >
          <v-simple-table dense>
            <template v-slot:default>
              <thead
                class="txt"
                style="background: #02c076; border-radius: 5px 5px 0 0"
              >
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
              <thead
                style="background: #ff5252; border-radius: 5px 5px 0 0"
                class="txt"
              >
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
  display: flex;
  align-items: center;
  background: rgb(0 0 0 / 20%);
}
.Headtxt {
  color: #fff;
}
</style>

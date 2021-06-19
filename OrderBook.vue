<template>
  <div class="orderbook">
    <v-card cols="12" height="600" width="400">
      <v-simple-table dense>
        <template v-slot:default>
          <thead>
            <tr>
              <th>قیمت</th>
              <th>حجم</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in orderbook.buy" :key="item">
              <td>{{ item.price }}</td>
              <td>{{ item.amount }}</td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>

      <v-simple-table dense>
        <template v-slot:default>
          <thead>
            <tr>
              <th>قیمت</th>
              <th>حجم</th>
            </tr>
          </thead>
          <tbody>
            <tr class="text-center" v-for="item in orderbook.sell" :key="item">
              <td>{{ item.price }}</td>
              <td>{{ item.amount }}</td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </v-card>
  </div>
</template>
<script>
export default {
  data: () => ({
    socket: null,
    orderbook: null,
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
    putComma(number) {
      const parts = number.toString().split(".");
      parts[0] = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      return parts.join(".");
    },
  },

  mounted() {
    this.startWebsocket();
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
</style>
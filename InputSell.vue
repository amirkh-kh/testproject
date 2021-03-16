<template>
  <v-app>
    <v-main>
      <v-card dark class="mt-4">
        <v-tabs v-model="tab" align-with-title>
          <v-tabs-slider color="yellow"></v-tabs-slider>

          <v-tab v-for="item in items" :key="item">
            {{ item }}
          </v-tab>
        </v-tabs>
        <v-tabs-items v-model="tab">
          <v-tab-item v-for="item in items" :key="item">
            <v-card flat>
              <v-card-text v-text="text"></v-card-text>
            </v-card> </v-tab-item
        ></v-tabs-items>
        <v-row>
          <!-- first box -->
          <v-col>
            <v-card
              id="Card"
              dark
              height="330"
              width="480"
              elevation="0"
              v-model="market"
            >
              <v-row
                style="
                  border: 0;
                  border-bottom: 2px solid grey;
                  margin: auto;
                  width: 90%;
                "
              >
                <v-col class="mx-3">
                  <h4>خرید بیت کوین</h4>
                </v-col>
                <v-spacer></v-spacer>
                <v-col class="mx-2">
                  <span
                    ><v-icon color="#e7ad0d">mdi-cash</v-icon>&nbsp;موجودی :
                    {{ InputValue }}</span
                  >
                </v-col>
              </v-row>

              <v-info-card>
                <v-text-field
                  style="width: 90%; margin: auto"
                  class="mt-2"
                  dense
                  solo
                  placeholder="قیمت"
                  suffix="ریال"
                ></v-text-field>

                <v-text-field
                  style="width: 90%; margin: auto"
                  dense
                  solo
                  placeholder="حجم"
                  suffix="BTC"
                >
                </v-text-field>
                <v-slider
                  inverse-label
                  class="mx-3 mt-2"
                  color="warning"
                  v-model="sellPick"
                  :tick-labels="LablePercent"
                  :max="5"
                  step="1"
                  ticks="always"
                  tick-size="4"
                ></v-slider>
                <v-btn
                  dense
                  dark
                  class="mt-5"
                  style="width: 90%; margin-bottom: 15px; margin-right: 20px"
                >
                  <a
                    href="#"
                    class="text-decoration-none"
                    style="color: gold; font-size: 20px"
                    v-on:click="Login"
                    >ورود</a
                  >
                  &nbsp;
                  <div style="font-size: 20px; color: grey">یا</div>
                  &nbsp;
                  <a
                    href="#"
                    class="text-decoration-none"
                    style="color: gold; font-size: 20px"
                    v-on:click="Register"
                    >ثبت نام</a
                  >
                </v-btn>
              </v-info-card>
            </v-card>
          </v-col>

          <!-- second box -->
          <v-col>
            <v-card dark height="330" width="480" elevation="0">
              <v-row
                style="
                  border: 0;
                  border-bottom: 2px solid grey;
                  margin: auto;
                  width: 90%;
                "
              >
                <v-col class="mx-3">
                  <h4>فروش بیت کوین</h4>
                </v-col>
                <v-spacer></v-spacer>
                <v-col class="mx-2">
                  <span
                    ><v-icon color="#e7ad0d">mdi-cash</v-icon>&nbsp;موجودی :
                    {{ InputValue }}</span
                  >
                </v-col>
              </v-row>

              <v-info-card>
                <v-text-field
                  style="width: 90%; margin: auto"
                  class="mt-2"
                  dense
                  solo
                  placeholder="قیمت"
                  suffix="ریال"
                ></v-text-field>

                <v-text-field
                  style="width: 90%; margin: auto"
                  dense
                  solo
                  placeholder="حجم"
                  suffix="BTC"
                ></v-text-field>
                <v-slider
                  inverse-label
                  class="mx-3 mt-2"
                  color="warning"
                  v-model="sellPick"
                  :tick-labels="LablePercent"
                  :max="5"
                  step="1"
                  ticks="always"
                  tick-size="4"
                ></v-slider>
                <v-btn
                  dense
                  dark
                  class="mt-5"
                  style="width: 90%; margin-bottom: 15px; margin-right: 20px"
                >
                  <a
                    href="#"
                    class="text-decoration-none"
                    style="color: gold; font-size: 20px"
                    v-on:click="Login"
                    >ورود</a
                  >
                  &nbsp;
                  <div style="font-size: 20px; color: grey">یا</div>
                  &nbsp;
                  <a
                    href="#"
                    class="text-decoration-none"
                    style="color: gold; font-size: 20px"
                    v-on:click="Register"
                    >ثبت نام</a
                  >
                </v-btn>
              </v-info-card>
            </v-card>
          </v-col>
        </v-row>
      </v-card>
    </v-main>
  </v-app>
</template>
<script>
export default {
  data: () => ({
    InputValue: 0,
    LablePercent: ["0%", "30%", "60%", "80%", "90%", "100%"],
    tab: null,
    items: ["Market", "Limit"],
    text: "#Card",
  }),
};
</script>
<style scoped>
</style>

<template>
  <v-app>
    <v-main>
      <v-card dark class="mt-4 mr-5">
        <v-row>
          <!-- first box -->
          <v-col>
            <v-form>
              <v-card
                class="mr-3"
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
                    required
                  ></v-text-field>

                  <v-text-field
                    style="width: 90%; margin: auto"
                    dense
                    solo
                    placeholder="حجم"
                    suffix="BTC"
                    required
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
                    @click="submit"
                    v-if="(Buy = !Buy)"
                    dense
                    dark
                    class="mt-5"
                    style="width: 90%; margin-bottom: 15px; margin-right: 20px"
                  >
                    <a
                      href="#"
                      class="text-decoration-none"
                      style="color: gold; font-size: 20px"
                      >ورود</a
                    >
                    &nbsp;&nbsp;
                    <div style="font-size: 20px">یا</div>
                    &nbsp;&nbsp;
                    <a
                      href="#"
                      class="text-decoration-none"
                      style="color: gold; font-size: 20px"
                      >ثبت نام</a
                    >
                  </v-btn>
                  <v-btn
                    v-else
                    dense
                    color="warning"
                    class="mt-5"
                    style="width: 90%; margin-bottom: 15px; margin-right: 20px"
                    >خرید</v-btn
                  >
                </v-info-card>
              </v-card>
            </v-form>
          </v-col>

          <!-- second box -->
          <v-col>
            <v-form>
              <v-card
                dark
                height="330"
                width="480"
                elevation="0"
                id="ChangeBtn"
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
                    required
                  ></v-text-field>

                  <v-text-field
                    style="width: 90%; margin: auto"
                    dense
                    solo
                    placeholder="حجم"
                    suffix="BTC"
                    required
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
                    v-if="(Sell = !Sell)"
                    dense
                    dark
                    class="mt-5"
                    style="
                      width: 90%;
                      margin-bottom: 15px;
                      margin-right: 20px;
                      font-size: 20px;
                    "
                  >
                    <a
                      href="#"
                      class="text-decoration-none"
                      style="color: gold; font-size: 20px"
                      >ورود</a
                    >
                    &nbsp;&nbsp;
                    <div style="font-size: 20px">یا</div>
                    &nbsp;&nbsp;
                    <a
                      href="#"
                      class="text-decoration-none"
                      style="color: gold; font-size: 20px"
                      >ثبت نام</a
                    >
                  </v-btn>
                  <v-btn
                    v-else
                    dense
                    color="red"
                    class="mt-5"
                    style="
                      width: 90%;
                      margin-bottom: 15px;
                      margin-right: 20px;
                      font-size: 20px;
                    "
                    >فروش</v-btn
                  >
                </v-info-card>
              </v-card>
            </v-form>
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
  }),
  methods: {
    submit() {
      this.$refs.form.submit();
    },
  },
};
</script>
<style scoped>
</style>

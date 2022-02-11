<template>
  <div class="about" style="display: flex; flex-wrap: wrap">
    <div v-for="item in user" :key="item.id" style="padding-left: 15%;">
      <v-card class='mx-auto'>
        <br>
        <div style="display: flex; margin-left: 20px; padding-right: 25px;">
          <img v-bind:src="item.photo" style="width: 120px; height: 120px; border-radius: 100%;">
          <div style="margin-left: 20px">
            <p style="padding-bottom: 0px; margin-bottom: 0px; font-size: 22px;">{{ item.name }}</p>
            <p style="color: #999999; padding-top: 0px">{{ item.city }}</p>
            <v-btn style="border-style: solid; border-color: #00b300; border-width: 2px; border-radius: 5px; background-color: white; color: #00b300" link v-bind:to="'/profile/' + item.id">Перейти в профиль</v-btn>
            <div style="height: 30px;"></div>
          </div>
        </div>
      </v-card>
      <br><br>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  data: () => ({
    user: []
  }),
  methods: {
    loadUser() {
      this.axios.get("http://37.77.104.246/api/jsonstorage/?id=cadd00cdd2c29efdd7eddd942dd231c8").then((response) => {
        this.user = response.data;
      });
    },
  },
  watch: {
    $route() {
      this.loadUser();
    },
  },
  mounted() {
    this.loadUser();
  },
};
</script>
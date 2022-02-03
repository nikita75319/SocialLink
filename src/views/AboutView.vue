<template>
  <div class="about" style="display: flex; flex-wrap: wrap">
    <div v-for="item in user" :key="item" style="padding-left: 15%;">
      <v-card class='mx-auto'>
        <br>
        <div style="display: flex; margin-left: 20px;">
          <img v-bind:src="'https://randomuser.me/api/portraits/men/' + item.id + '.jpg'" style="width: 20%; height: 20%; border-radius: 100%;">
          <div style="margin-left: 20px">
            <p style="padding-bottom: 0px; margin-bottom: 0px; font-size: 22px;">{{ item.name }}</p>
            <p style="color: #999999; padding-top: 0px">{{ item.address.city }}</p>
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
    user: {
      "id": 2,
      "name": "Ervin Howell",
      "username": "Antonette",
      "email": "Shanna@melissa.tv",
      "address": {
        "street": "Victor Plains",
        "suite": "Suite 879",
        "city": "Wisokyburgh",
        "zipcode": "90566-7771",
        "geo": {
          "lat": "-43.9509",
          "lng": "-34.4618"
        }
      },
      "phone": "010-692-6593 x09125",
      "website": "anastasia.net",
      "company": {
        "name": "Deckow-Crist",
        "catchPhrase": "Proactive didactic contingency",
        "bs": "synergize scalable supply-chains"
      }
    }
  }),

  methods: {
    loadUser() {
      this.axios.get("http://jsonplaceholder.typicode.com/users").then((response) => {
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
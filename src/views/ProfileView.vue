<template>
  <div>
     <div>
        <v-row class="text-left">
            <v-col cols="10">
                <h1 class="green--text text--darken-2">
                    <v-icon large color="green darken-2">mdi-account-outline</v-icon>
                    {{ user.name }}
                </h1>
            </v-col>
        </v-row>
        <v-row class="text-left">
            <v-col cols="2">
                <img v-bind:src="'https://randomuser.me/api/portraits/men/' + user.id + '.jpg'" style="max-width: 100%">
            </v-col>
            <v-col cols="10" class="text-left">
                <p>
                    Веб-сайт: <a href="..." target="_blank">{{ user.website }}</a>
                </p>
                <p>
                    E-mail: <a href="mailto:..."> {{ user.email }}</a>
                </p>
                <p>
                    Город: {{ user.address.city }}
                </p>
                <p>
                    Место работы: {{ user.company.name }}
                </p>
            </v-col>
        </v-row>

        <h1 class="black--text text--darken-2">Публикации</h1>

        <v-row>
          <v-col cols="9">
            <br>
            <div v-for="item in post" :key="item">
              <v-card class="mx-auto">
                <div style="height: 10px;" />
                <div style="display: flex; justify-content: start; margin-left: 10px;">
                  <img v-bind:src="'https://randomuser.me/api/portraits/men/' + user.id + '.jpg'" style="max-width: 5%; border-radius: 100%; margin: 10px; ">
                  <div>
                    <v-card-title v-text="item.title" style="padding-bottom: 0px;"></v-card-title>
                    <p style="padding-top: 0px; padding-left: 15px">Автор: {{ user.name }}</p> 
                  </div>
                </div>
                <br>
                <p style="margin-left: 50px;">{{ item.body}}</p>
                <div style="display: flex; justify-content: end; margin-right: 20px;">
                  <v-btn icon color="gray">
                    <v-icon>mdi-heart</v-icon>
                  </v-btn>

                  <v-btn icon color="gray">
                    <v-icon>mdi-star</v-icon>
                  </v-btn>

                  <v-btn icon color="gray">
                    <v-icon>mdi-share</v-icon>
                  </v-btn>
                </div>
                <div style="height: 30px" />
              </v-card>
              <br>
            </div>
          </v-col>
        </v-row>

    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    currentId: null,
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
    },
    post: {

    },
  }),

  methods: {
    loadUser() {
      this.axios
        .get("https://jsonplaceholder.typicode.com/users/" + this.currentId)
        .then((response) => {
          this.user = response.data;
        });
    },
    loadPost() {
      this.axios
        .get("http://jsonplaceholder.typicode.com/posts?userId=" + this.currentId)
        .then((response) => {
          this.post = response.data;
        });
    },
  },

  watch: {
    $route() {
      this.currentId = this.$route.params.id;
      this.loadUser();
      this.loadPost();
    },
  },

  mounted() {
    this.currentId = this.$route.params.id;
    this.loadUser();
    console.log(this.currentId);
    this.loadPost();
  },
};
</script>

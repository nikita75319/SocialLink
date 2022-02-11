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
                <img v-bind:src="user.photo" style="max-width: 100%">
            </v-col>
            <v-col cols="10" class="text-left">
                <p>
                    Веб-сайт: <a href="..." target="_blank">{{ user.website }}</a>
                </p>
                <p>
                    E-mail: <a href="mailto:..."> {{ user.email }}</a>
                </p>
                <p>
                    Город: {{ user.city }}
                </p>
                <p>
                    Место работы: {{ user.company }}
                </p>
            </v-col>
        </v-row>

        <h1 class="black--text text--darken-2">Публикации</h1>

        <v-row>
          <v-col cols="9">
            <br>
            <v-card width="600px" class="mt-12 pa-10" >
                <v-card-title> Новый пост</v-card-title>
                <v-text-field label="Название поста" v-model="title" outlined></v-text-field>
                <v-text-field label="Содержание" v-model="content" outlined></v-text-field>
                <v-btn @click="newPost">Опубликовать</v-btn>
            </v-card>
            <br>
            <br>
            <div v-for="item in post" :key="item.id">
              <v-card class="mx-auto" v-if="item.id == currentId">
                <div style="height: 10px;" />
                <div style="display: flex; justify-content: start; margin-left: 10px;">
                  <img v-bind:src="item.photo" style="max-width: 50px; max-height: 50px; border-radius: 100%; margin: 10px; ">
                  <div>
                    <v-card-title v-text="item.title" style="padding-bottom: 0px;"></v-card-title>
                    <p style="padding-top: 0px; padding-left: 15px">Автор: {{ item.name }}</p> 
                  </div>
                </div>
                <br>
                <p style="margin-left: 50px;">{{ item.content}}</p>
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
    currentId: 0,
    user: {},
    users: [],
    post: {},
    title: "",
    content: "",
  }),
  props: ["mainUser"],
  methods: {
    loadUser() {
      this.axios
        .get("http://37.77.104.246/api/jsonstorage/?id=cadd00cdd2c29efdd7eddd942dd231c8")
        .then((response) => {
          this.users = response.data;
          for (let i in this.users) {
            if(this.users[i].id == this.currentId) {
              this.user = this.users[i];
              console.log("photo ");
              console.log(this.user.photo);
            }
          }
        });

    },
    loadPost() {
      this.axios
        .get("http://37.77.104.246/api/jsonstorage/?id=4fdecb61152acbde0e495f9ed4f5c97c")
        .then((response) => {
          this.post = response.data;

        });
    },
    newPost() {
      this.axios
        .get("http://37.77.104.246/api/jsonstorage/?id=4fdecb61152acbde0e495f9ed4f5c97c")
        .then((response) => {
          let posts = response.data;
          let id = this.currentId;
          let newPost = {
            "id": id,
            "title": this.title,
            "content": this.content,
            "name": this.mainUser.name,
            "photo": this.mainUser.photo,
          };
          posts.push(newPost);

          this.axios ({
            method: 'put',
            url: 'http://37.77.104.246/api/jsonstorage/?id=4fdecb61152acbde0e495f9ed4f5c97c',
            data: posts,
          }).then(() => {
            console.log("new post");
            this.loadPost();
          });
          
        });
      
    }
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
    this.loadPost();
  },
};
</script>
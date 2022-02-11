<template>
    <div class="d-flex justify-center">
        <v-card width="600px" class="mt-12 pa-10">
            <v-card-title> Зарегeстрируйтесь</v-card-title>
            <v-text-field label="Введите логин" v-model="login" outlined></v-text-field>
            <v-text-field label="Введите пароль" v-model="password" outlined></v-text-field>
            <v-text-field label="Введите имя" v-model="name" outlined></v-text-field>
            <v-text-field label="Введите вебсайт" v-model="website" outlined></v-text-field>
            <v-text-field label="Введите email" v-model="email" outlined></v-text-field>
            <v-text-field label="Введите город" v-model="city" outlined></v-text-field>
            <v-text-field label="Введите компанию" v-model="company" outlined></v-text-field>
            <v-text-field label="Введите ссылку на фото" v-model="photo" outlined></v-text-field>
            <v-btn @click="registr"> Зарегистрироваться </v-btn>
        </v-card>
    </div>
</template>

<script>
/* eslint-disable */

export default {
    data: () => ({
        login: "",
        password: "",
        name: "",
        webcite: "",
        email: "",
        city: "",
        company: "",
        photo: "",
        
    }),
    methods: {
        registr() {
            this.axios.get('http://37.77.104.246/api/jsonstorage/?id=cadd00cdd2c29efdd7eddd942dd231c8')
                .then(
                    (response) => {
                        let users = response.data;
                        let id = users.length + 1;
                        let user = {
                            "id": id,
                            "login": this.login,
                            "password": this.password,
                            "name": this.name,
                            "webcite": this.webcite,
                            "email": this.email,
                            "city": this.city,
                            "company": this.company,
                            "photo": this.photo,
                        };
                        users.push(user);
                        console.log(users);
                        console.log(id);

                        this.axios ({
                            method: 'put',
                            url: 'http://37.77.104.246/api/jsonstorage/?id=cadd00cdd2c29efdd7eddd942dd231c8',
                            data: users,
                        }).then((response) => {
                            console.log("end.");
                            this.$router.push('/');
                        })
                    }
                );
        }
    }
};
</script>
<template>
  <v-app>
    <v-main>
      <v-container class="form-container">
        <h1>App Keo</h1>
        <v-row>
          <v-col cols="12" sm="4">
            <v-select
                v-model="profession"
                :items="professions"
                label="Profession"
                outlined
                dense
            ></v-select>
          </v-col>
          <v-col cols="12" sm="4">
            <v-select
                v-model="city"
                :items="cities"
                label="City"
                outlined
                dense
            ></v-select>
          </v-col>
          <v-col cols="12" sm="4">
            <v-select
                v-model="salary"
                :items="salaries"
                label="Salary"
                outlined
                dense
            ></v-select>
          </v-col>
          <v-col cols="12">
            <v-text-field
                v-model="email"
                label="Email"
                placeholder="Enter your email"
                outlined
                dense
            ></v-text-field>
          </v-col>
        </v-row>
        <v-row justify="center">
          <v-col cols="12" sm="6" md="4">
            <v-btn
                color="success"
                @click="subscribe"
                block="true"

                :disabled="isSubscribed"
                class="mb-2"
            >
              Subscribe
            </v-btn>
            <v-btn
                color="error"
                @click="unsubscribe"
                block="true"

                :disabled="!isSubscribed"
            >
              Unsubscribe
            </v-btn>
            <v-btn
                color="primary"
                @click="show_vacancies"
                block="true"
            >
              Просмотреть вакансии
            </v-btn>
          </v-col>
        </v-row>
        <v-row>
          <Vacancies/>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Vacancies from "@/components/VacanciesComp.vue";
export default {
  name: 'App',
  components: {
    Vacancies
  },
  data() {
    return {
      profession: '',
      professions: ['Backend', 'Frontend', 'Fullstack', 'Manager', 'Analyst'],
      city: '',
      cities: ['Москва', 'Санкт-Петербург', 'Екатеринбург', 'Челябинск', 'Remote'],
      salary: '',
      salaries: ['40,000', '60,000', '80,000', '100,000'],
      email: '',
      isSubscribed: false
    };
  },
  methods: {
    subscribe() {
      this.isSubscribed = true;
      alert("Subscribed with " + this.email);
    },
    unsubscribe() {
      this.isSubscribed = false;
      alert("Unsubscribed");
    },
    show_vacancies() {
      //this.isSubscribed = false;
      alert("Showing soon...");
    }
  }
}
</script>

<style scoped>
.form-container {
  padding-top: 5vh;
  padding-left: 30vh;
  padding-right: 30vh;
  text-align: center;
}

/* Styling the buttons to be in a vertical list */
.v-btn {
  margin-top: 10px;
}

/* Adjusting the styles of the select inputs for a better user experience */
.v-select, .v-text-field {
  margin-bottom: 16px;
}
</style>

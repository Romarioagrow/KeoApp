<template>
  <v-app>
    <v-main>
      <v-container class="form-container">
        <h1>App Keo</h1>
        <v-row>
          <v-col cols="12" sm="3">
            <v-text-field
                label="Profession"
                v-model="profession"
                name="Профессия"
            ></v-text-field>
          </v-col>
          <v-col cols="12" sm="3">
            <v-select
                v-model="city"
                :items="cities"
                label="City"
                outlined
                dense
            ></v-select>
          </v-col>
          <v-col cols="12" sm="3">
            <v-select
                v-model="salary"
                :items="salaries"
                label="Salary"
                outlined
                dense
            ></v-select>
          </v-col>
          <v-col cols="12" sm="3">
            <input type="checkbox" id="checkbox"  v-model="isRemote">
            <label for="checkbox">{{ "Remote" }}</label>
          </v-col>
        </v-row>
        <v-row>
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
<!--          <Vacancies/>-->
          <v-row>
            <h2>
              Vacancies
            </h2>
          </v-row>
          <v-row>
            <v-btn slim="true">
              Back
            </v-btn>
          </v-row>
          <v-row>
            <v-col cols="12">
              <v-text-field v-model="vacancyId" label="Vacancy ID"></v-text-field>
              <v-btn @click="fetchData">Fetch Data</v-btn>
            </v-col>
          </v-row>
          <v-row>
            <!-- Отображение данных здесь -->
            <div v-if="responseData">
              <pre>{{ responseData }}</pre>
            </div>
          </v-row>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";
export default {
  name: 'App',
  components: {
    //Vacancies
  },
  data() {
    return {
      profession: '',
      professions: ['Backend', 'Frontend', 'Fullstack', 'Manager', 'Analyst'],
      city: '',
      cities: ['Москва', 'Санкт-Петербург', 'Екатеринбург', 'Челябинск', 'Remote'],
      salary: '',
      salaries: ['40000', '60000', '80000', '100000', '150000', '200000' ],
      email: '',
      isSubscribed: false,

      // fetches
      isRemote: false,
      vacancyId: '',
      responseData: null,
      apiData: {
        baseUrl: 'https://api.hh.ru/vacancies?',

      }
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
      alert("Showing soon...");
    },
    fetchData() {
      //const apiUrl = `https://api.hh.ru/negotiations/somecollection?vacancy_id=${this.vacancyId}`;
      //const apiUrl = `https://api.hh.ru/vacancies?area=113`;
      /*
      *
      * Саня, [26.11.2023 20:45]
https://api.hh.ru/vacancies?remote=true&salary_from=150000

Саня, [26.11.2023 20:46]
https://api.hh.ru/vacancies?remote=true

Саня, [26.11.2023 20:46]
https://api.hh.ru/vacancies?text="Аналитик"&area=104&salary=100000
      *
      *
      *
      * 1 сосква
2 питер
3 екб
104 чилик
      * */

       let profession = this.profession;
       let city = '';
       let salary = this.salary;
       let isRemote = this.isRemote;

//      cities: ['Москва', 'Санкт-Петербург', 'Екатеринбург', 'Челябинск', 'Remote'],

      switch (this.city) {
         case "Москва": city = '1'; break
         case "Санкт-Петербург": city = '2'; break
         case "Екатеринбург": city = '3'; break
         case "Челябинск": city = '104'; break
      }

      const apiUrl = this.apiData.baseUrl + 'text=' + profession + (isRemote ? '&remote=true' : '') + '&area=' + city + '&salary=' + salary;

      console.log(apiUrl);

      // Сам запрос на HH
      axios.get(apiUrl)
          .then(response => {
            this.responseData = response.data;
          })
          .catch(error => {
            console.error("Error fetching data:", error);
            this.responseData = null;
          });
    },
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


.checkbox-active .v-label {
  font-weight: bold; /* Сделать текст жирным при активации чекбокса */
}

/* Стили для чекбокса, когда он не активен */
.v-checkbox--is-disabled .v-icon,
.v-checkbox:not(.v-checkbox--is-disabled) .v-icon:not(.v-icon--disabled) {
  color: rgba(0, 0, 0, 0.54); /* Серый цвет для иконки */
}

/* Стили для чекбокса, когда он активен */
.v-checkbox.v-input--is-checked .v-icon {
  color: #7B1FA2; /* Цвет при активации (в вашем случае deep-purple accent-2) */
}

.v-checkbox .v-input--selection-controls__ripple {
  opacity: 0.12; /* Определяет непрозрачность ripple-эффекта */
}

/* Увеличить размер иконки чекбокса */
.v-checkbox .v-icon {
  font-size: 24px; /* Размер иконки */
}



</style>

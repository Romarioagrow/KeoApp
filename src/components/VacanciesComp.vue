<template>
    <v-container>
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
    </v-container>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      vacancyId: '',
      responseData: null
    };
  },
  methods: {
    fetchData() {
      //const apiUrl = `https://api.hh.ru/negotiations/somecollection?vacancy_id=${this.vacancyId}`;
      const apiUrl = `https://api.hh.ru/vacancies?area=113`;

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
    // Методы для отправки данных на почту и другие действия
  }
}
</script>

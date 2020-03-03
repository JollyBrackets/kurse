<template>
  <div id="app" class="h-100">
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="#">Kurs Anwesenheiten - Bechterew</b-navbar-brand>
    </b-navbar>

    <b-container fluid class="h-100">
      <b-row class="h-100">
        <b-col sm="2" class="p-0 border-right">
          <h6 class="pt-3 pl-3 text-uppercase text-primary">Meine Kurse</h6>
          <b-list-group flush>
            <b-list-group-item
              v-for="kurs in kurse"
              :key="kurs.id"
              @click="selectedKurs = kurs"
              button 
              :active="kurs === selectedKurs"
              class="d-flex justify-content-between align-items-center"
            >
              <span>{{ kurs.name }}</span>
              <b-icon icon="chevron-right" />
            </b-list-group-item>
          </b-list-group>
        </b-col>

        <b-col sm="2" class="p-0 border-right">
          <h6 class="pt-3 pl-3 text-uppercase text-primary">Termine</h6>

          <b-list-group flush v-if="selectedKurs">
            <b-list-group-item
              v-for="termin in selectedKurs.termine"
              :key="termin"
              @click="selectedDate = termin"
              button 
              :active="selectedDate === termin"
              class="d-flex justify-content-between align-items-center"
            >
              <span>{{ termin }}</span>
              <b-icon icon="chevron-right" />
            </b-list-group-item>
          </b-list-group>
          
          <p v-else>
            Kurse auswählen
          </p>
        </b-col>
        <b-col class="p-0">
          <template v-if="selectedKurs && selectedDate">
            <h6 class="pt-3 pl-3 text-uppercase text-primary">Leiter</h6>
            <b-form-select
              v-model="selectedLeiter"
              :options="selectedKurs.leiter"
            />

            <h6 class="pt-3 pl-3 text-uppercase text-primary">Anwesenheiten</h6>

            <b-list-group flush>
              <b-list-group-item
                v-for="teilnehmer in selectedKurs.teilnehmer"
                :key="teilnehmer"
                button 
                class="d-flex justify-content-between align-items-center"
              >
                <span>{{ teilnehmer }}</span>
                <b-icon icon="check-box" scale="1.2" />
              </b-list-group-item>
            </b-list-group>

             <b-button variant="primary" class="float-right mt-5 mr-3">Abschicken</b-button>
          </template>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import data from './data.js'
export default {
  data () {
    return {
      kurse: data.kurse,
      selectedKurs: null,
      selectedDate: null,
      selectedLeiter: null
    }
  },
}
</script>

<style>
html, body {
  height: 100%;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

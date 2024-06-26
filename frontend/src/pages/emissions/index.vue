<script setup lang="ts">
import { storeToRefs } from 'pinia'
import { useCountryEmissionStore } from '@/stores/countryEmission'

const countryEmissionStore = useCountryEmissionStore()
const { rawCo2EmissionsData, rawGhgEmissionsData } = storeToRefs(countryEmissionStore)

const co2EmissionsDataSearch = ref('')
const ghgEmissionsDataSearch = ref('')

const searchPlaceholder = 'Search...'

const headers = [
  { title: 'Country', value: 'country', sortable: true, width: '25%' },
  { title: 'Year', value: 'year', sortable: true, width: '25%' },
  { title: 'ISO Code', value: 'iso_code', sortable: true, width: '25%' },
]

const co2EmissionsDataHeaders = [
  ...headers,
  { title: 'Annual CO₂ emissions (Million Tonnes)', value: 'co2', sortable: true, width: '25%' },
]

const ghgEmissionsDataHeaders = [
  ...headers,
  { title: 'Total greenhouse gas emissions (Million Tonnes of carbon dioxide-equivalents)', value: 'total_ghg', sortable: true, width: '25%' },
]
</script>

<template>
  <v-row>
    <v-col cols="12">
      <v-data-table
        :headers="co2EmissionsDataHeaders"
        :items="rawCo2EmissionsData"
        :search="co2EmissionsDataSearch"
      >
        <template #top>
          <v-toolbar flat>
            <v-toolbar-title>Co2 Emissions Data</v-toolbar-title>

            <v-text-field
              v-model="co2EmissionsDataSearch"
              :placeholder="searchPlaceholder"
              clearable
              hide-details
            />
          </v-toolbar>
        </template>
      </v-data-table>
    </v-col>
    <v-col cols="12">
      <v-data-table
        :headers="ghgEmissionsDataHeaders"
        :items="rawGhgEmissionsData"
        :search="ghgEmissionsDataSearch"
      >
        <template #top>
          <v-toolbar flat>
            <v-toolbar-title>Ghg Emissions Data</v-toolbar-title>
            <v-text-field
              v-model="ghgEmissionsDataSearch"
              :placeholder="searchPlaceholder"
              clearable
              hide-details
            />
          </v-toolbar>
        </template>
      </v-data-table>
    </v-col>
  </v-row>
</template>

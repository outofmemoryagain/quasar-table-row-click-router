<template>
  <q-page class="row items-center justify-evenly">
    <q-table
      title="Treats"
      :data="data"
      :columns="columns"
      row-key="name" @row-click="viewDessert"
    />
  </q-page>
</template>

<script lang="ts">
import Vue from 'vue'
import Component from 'vue-class-component'
import { getDesserts, Dessert } from 'src/api/DessertsApi'

@Component
export default class Index extends Vue {
  public columns: Array<RowColumn<Dessert, unknown>> = [
    {
      name: 'name',
      required: true,
      label: 'Dessert (100g serving)',
      align: 'left',
      field: row => row.name,
      format: val => `${val}`,
      sortable: true
    },
    { name: 'calories', align: 'center', label: 'Calories', field: 'calories', sortable: true },
    { name: 'fat', label: 'Fat (g)', field: 'fat', sortable: true },
    { name: 'carbs', label: 'Carbs (g)', field: 'carbs' },
    { name: 'protein', label: 'Protein (g)', field: 'protein' },
    { name: 'sodium', label: 'Sodium (mg)', field: 'sodium' },
    { name: 'calcium', label: 'Calcium (%)', field: 'calcium', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) },
    { name: 'iron', label: 'Iron (%)', field: 'iron', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) }
  ]

  public data = getDesserts();

  public viewDessert (evt: Event, dessert: Dessert) {
    this.$router.push('/dessert/' + dessert.name)
  }
}

export interface RowColumn<TRow, TColumn> {
  name: string;
  required?: boolean;
  align?: 'center' | 'left' | 'right';
  label?: string;
  field?: string | ((row: TRow) => string);
  sortable?: boolean;
  sort?: ((a: string, b: string) => number);
  format?: ((val: TColumn) => string);
}
</script>

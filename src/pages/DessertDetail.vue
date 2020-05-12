<template>
  <q-page class="row items-center justify-evenly">
    <q-card v-if="dessert">
      <q-list dense>
        <q-item-section>{{ dessert.name }}</q-item-section>
        <q-item-section>
          <q-item-label>Calories: {{ dessert.calories }}</q-item-label>
        </q-item-section>
      </q-list>
    </q-card>
  </q-page>
</template>

<script lang="ts">
import Vue from 'vue'
import Component from 'vue-class-component'
import { Prop } from 'vue-property-decorator'
import { Dessert, getDessert } from '../api/DessertsApi'

@Component
export default class DessertDetail extends Vue {
  @Prop() public readonly name!: string
  public dessert? = {} as Dessert;

  public async load () {
    this.dessert = await getDessert(this.name)
  }

  async mounted () {
    await this.load()
  }
}
</script>

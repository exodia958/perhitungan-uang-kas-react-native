<script setup lang="ts">
import { emit } from 'process';
import { ref } from 'vue'

interface Props {
  total: number,
  toggleValue: boolean
}

interface selectCategories {
  label: string,
  value:  number
}

const props = withDefaults(defineProps<Props>(),{
  total: 0
})

const account1 = ref(50);
const account2 = ref(10);
const account3 = ref(10);
const account4 = ref(10);
const account5 = ref(10);
const account6 = ref(10);

const expanded = ref(false)
const toggle = ref(false);

const emit = defineEmits(['accountsPercentajes', 'specificAccount', 'update:toggleValue'])

const sendEmitvalues = ()=>{
  if(!toggle.value){
    console.log(account1.value);

    emit('accountsPercentajes', [account1.value, account2.value, account3.value, account4.value, account5.value, account6.value])
  }
}

const categoriesnew = ref<selectCategories[]>([
  { label: 'Keperluar Basic', value: 0},
  { label: 'Finansial', value: 1},
  { label: 'Pelatihan', value: 2},
  { label: 'Tabungan', value: 3},
  { label: 'Sedekah', value: 4},
  { label: 'Healing', value: 5}]);

const categoryselected = ref<selectCategories | null>(null);

</script>

<template>
  <q-btn
        color="grey"
        round
        flat
        dense
        :icon="expanded ? 'keyboard_arrow_up' : 'keyboard_arrow_down'"
        @click="expanded = !expanded"
        label="Presentase Akun"
      />
  <q-slide-transition>
    <div v-if="expanded">
      <q-separator />
      <q-card-section class="text-subitle2">
        <div>
          <q-toggle v-model="toggle" label="tambah ke akun tertentu" @update:model-value="$emit('update:toggleValue', toggle)"/>
          <div v-show="!toggle">
            <div class="q-mb-sm">
              <q-input ref="account11" type="number" suffix="%" outlined v-model.number="account1" @update:model-value="sendEmitvalues" label="Presentase Keperluar Basic" :hint="(account1*props.total/100).toString()"/>
            </div>
            <div class="q-mb-sm">
              <q-input ref="account21" type="number" suffix="%" outlined v-model.number="account2" @update:model-value="sendEmitvalues" label="Presentase Finansial" :hint="(account2*props.total/100).toString()"/>
            </div>
            <div class="q-mb-sm">
              <q-input ref="account31" type="number" suffix="%" outlined v-model.number="account3" @update:model-value="sendEmitvalues" label="Pelatihan" :hint="(account3*props.total/100).toString()"/>
            </div>
            <div class="q-mb-sm">
              <q-input ref="account41" type="number" suffix="%" outlined v-model.number="account4" @update:model-value="sendEmitvalues" label="Tabungan" :hint="(account4*props.total/100).toString()"/>
            </div>
            <div class="q-mb-sm">
              <q-input ref="account51" type="number" suffix="%" outlined v-model.number="account5" @update:model-value="sendEmitvalues" label="Sedekah" :hint="(account5*props.total/100).toString()"/>
            </div>
            <div class="q-mb-sm">
              <q-input ref="account61" type="number" suffix="%" outlined v-model.number="account6" @update:model-value="sendEmitvalues" label="Healing" :hint="(account6*props.total/100).toString()"/>
            </div>
          </div>
          <div v-show="toggle">
            <q-select ref="categoryref" outlined v-model="categoryselected" :options="categoriesnew" label="Cuenta"
              :rules="[val => val || !toggle || 'pilihkategori']" lazy-rules @update:model-value="$emit('specificAccount', categoryselected)"/>
          </div>
        </div>
      </q-card-section>
    </div>
  </q-slide-transition>

</template>

<style scoped>

</style>

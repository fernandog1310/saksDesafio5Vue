<template>
  <div>
    <div v-if="imoveis.length > 1">
      <div v-if="showLabel">
        Imovel*
      </div>
      <imobiliaria-select
        v-bind="$attrs"
        name="imovel"
        rules="required"
        :class="showLabel ? 'mt--md' : ''"
        @on-change="onChange">
        <option :value="null" disabled>Selecione um imovel...</option>
        <option
          v-for="imovel in imoveis"
          :key="imovel.id"
          :value="imovel.id">
          {{ imovel.titulo }}
        </option>
      </imobiliaria-select>
    </div>
    <div v-else class="mb-3 mt-4">
      <imobiliaria-p color="danger">
        *Você não possui imoveis cadastrados
        <imobiliaria-button @click="onCreate">
          Criar Imovel
        </imobiliaria-button>
      </imobiliaria-p>
    </div>
  </div>
</template>

<script>
import { fetchImoveis } from '@/modules/imovel/imovel.service';
import { goToCreateImovel } from '@/modules/imovel/imovel.routes';

export default {
  name: 'ImobiliariaImoveiselect',
  props: {
    showLabel: {
      type: Boolean,
      default: true,
    },
    isFilter: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      imoveis: [],
    };
  },
  created() {
    this.onfetch();
  },
  methods: {
    onfetch() {
      fetchImoveis()
        .then(data => {
          this.imoveis = data.data;
        })
        .catch(() => {
          this.imoveis = null;
        });
    },
    onChange(id) {
      this.$emit('on-change', { id });
    },
    onCreate() {
      goToCreateImovel(this.$router);
    },
  },
};
</script>

<template>
  <router-link :to="to">
    <slot />
  </router-link>
</template>
<script>
import { TIPOIMOVEIS_URL } from '@/modules/tipoImovel/tipoImovel.constants';

export default {
  name: 'ImobiliariaTipoImovelLink',
  props: {
    id: {
      type: Number,
      required: true,
    },
    action: {
      type: String,
      default: 'view',
      validator(action) {
        return action && ['view', 'edit'].includes(action);
      },
    },
  },
  computed: {
    to() {
      return {
        name: TIPOIMOVEIS_URL[this.action].name,
        path: TIPOIMOVEIS_URL[this.action].path,
        params: {
          id: this.id,
        },
      };
    },
  },
};
</script>

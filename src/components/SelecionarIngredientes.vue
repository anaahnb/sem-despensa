<script lang="ts">

import { obterCategorias } from '@/http/index';
import type ICategoria from '@/interfaces/ICategorias';
import CardCategoria from './CardCategoria.vue';
import BotaoPrincipal from './BotaoPrincipal.vue';

export default {
    data() {
        return {
            categorias: [] as ICategoria[]
        };
    },
    async created() {
        this.categorias = await obterCategorias();
    },
    components: { CardCategoria, BotaoPrincipal },
    emits: ['adicionarIngrediente', 'removerIngrediente', 'buscarReceitas'],
}
</script>


<template>
  <section class="selecionar-ingredientes">
    <h1 class="subtitulo-lg titulo-ingredientes">Ingredientes</h1>

    <p class="paragrafo instrucoes">
      Selecione abaixo os ingredientes que você quer usar nesta receita. Consideramos que você tem em casa sal, pimenta e água.
    </p>

    <ul class="categorias">
      <li v-for="categoria in categorias" :key="categoria.nome">
        <CardCategoria :categoria="categoria" @adicionar-ingrediente="$emit('adicionarIngrediente', $event)" @remover-ingrediente="$emit('removerIngrediente', $event)"/>
      </li>
    </ul>

    <BotaoPrincipal texto="Buscar receitas!" @click="$emit('buscarReceitas')" />
  </section>
</template>

<style scoped>
.selecionar-ingredientes {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-ingredientes {
  display: block;
  margin-bottom: 1.5rem;
  color: var(--verde);

}

.instrucoes {
  margin-bottom: 2rem;
  max-width: 36rem;
  text-align: center;
}

.categorias {
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

</style>



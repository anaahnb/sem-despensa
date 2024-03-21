<script lang="ts">
import type ICategoria from '@/interfaces/ICategorias';
import type { PropType } from 'vue';
import Tag from './Tag.vue';
import IngredienteSelecionavel from './IngredienteSelecionavel.vue';

export default {
    props: {
        categoria: { type: Object as PropType<ICategoria>, required: true }
    },
    components: { Tag, IngredienteSelecionavel },
    emits: ['adicionarIngrediente', 'removerIngrediente']
}
</script>

<template>
  <article class="categoria">
    <header class="categoria__cabecalho">
      <h2 class="paragrafo categoria__nome">
        {{ categoria.nome }}
      </h2>
    </header>

    <ul class="categoria__ingredientes">
      <li v-for="ingrediente in categoria.ingredientes" :key="ingrediente">
        <IngredienteSelecionavel @adicionar-ingrediente="$emit('adicionarIngrediente', $event)" @remover-ingrediente="$emit('removerIngrediente', $event)" :ingrediente="ingrediente" />
      </li>
    </ul>

  </article>
</template>

<style scoped>
  .categoria {
    width: 19.5rem;
    padding: 1rem;
    border-radius: 0.5rem;
    background: var(--branco);
    height: 100%;

    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
  }

  .categoria__cabecalho {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
  }

  .categoria__imagem {
    width: 3.5rem;
  }

  .categoria__nome {
    text-align: center;
    color: var(--cinza);
    font-weight: 700;
  }

  .categoria__ingredientes {
    display: flex;
    justify-content: center;
    gap: 0.5rem;
    flex-wrap: wrap;
  }

</style>

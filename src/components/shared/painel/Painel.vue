<template>

    <div @click="disparaAcao()" :class="changeStyle">
      <transition name="painel-fade">
        <div class="painel-conteudo" v-show="visibily">
          <slot v-show="activeCard"></slot>
        </div>
      </transition>
      <div
        @dblclick="visibily = !visibily"
        >
        <p v-if="activeCard"> {{ titulo }}</p>
        <p v-else class="close-card">?</p>
      </div>

    </div>

</template>

<script>

export default {
  props: {
    titulo: {
      type: String
    },
    activeCard: {
      type: Boolean
    }
  },
  data() {
    return {
      visibily: true
    }
  },
  methods: {
    disparaAcao() {
      this.$emit('cardSelect');
    }
  },
  computed: {
    changeStyle() {
      if (this.activeCard) {
        return 'painel';
      } else {
        return 'painel color-close-card';
      }
    }
  }
}
</script>
<style scoped>
/* estilo do painel */

.painel {
 padding: 0 auto;
 display: inline-block;
 margin: 5px;
 box-shadow: 5px 5px 10px #999;
 width: 284px;
 height: 100%;
 vertical-align: top;
 text-align: center;
 border-radius: 3px;

}

.color-close-card {
  background-color: #FFC107;
}

.close-card {
  font-size: 70px;
  font-weight: bold;
  margin: 76px 0;
}

.painel .painel-titulo {
 text-align: center;
 margin: 0;
 padding: 10px;
}

/* painel-fade-enter // antes do elemento ser incluído ou removido, o estado atual
painel-fade-enter-active // quando o elemento esta sendo incluído
painel-fade-leave-active // quando o elemento esta sendo removido */

.painel-fade-enter, .painel-fade-leave-active {
  opacity: 0
}

.painel-fade-enter-active, .painel-fade-leave-active {
  transition: opacity .4s
}
</style>

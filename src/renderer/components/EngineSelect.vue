<template>
  <div class="container">
    <div
      class="logo"
    >
      <div
        class="image"
        :style="{ backgroundImage: engineLogo }"
      />
    </div>
    <Multiselect
      v-model="selected"
      class="multiselect"
      label="name"
      track-by="name"
      :options="availableEngines"
      :allow-empty="false"
      :show-labels="false"
      :placeholder="selected.name"
    />
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Multiselect from 'vue-multiselect'
import defaultLogo from '../assets/images/engines/chess_engine.svg'

export default {
  name: 'EngineSelect',
  components: { Multiselect },
  data () {
    return {
      selected: null // this will be set on created
    }
  },
  computed: {
    engineLogo () {
      return `url(${this.selectedEngine.logo || defaultLogo})`
    },
    ...mapGetters(['availableEngines', 'selectedEngine'])
  },
  watch: {
    selected () {
      this.$store.dispatch('changeEngine', this.selected.name)
    },
    selectedEngine () {
      this.selected = this.selectedEngine
    }
  },
  created () {
    this.selected = this.selectedEngine
  }
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.logo {
  flex-basis: 120px;
  flex-shrink: 0;
  flex-grow: 0;
  margin-right: 5px;
}
.logo .image {
  box-sizing: content-box;
  width: 120px;
  height: 60px;
  background-color: #fff;
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
  border-radius: 5px;
}

.multiselect {
  flex-basis: auto;
  flex-shrink: 1;
  flex-grow: 1;
}
</style>

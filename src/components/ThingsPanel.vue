<template>
  <div class="current-section" v-if="$q.platform.is.desktop">
    <q-layout>
      <q-header elevated>
        <q-toolbar>
          <q-toolbar-title>{{$t('things').toUpperCase()}}</q-toolbar-title>
          <q-btn flat round dense icon="close" @click="closeWindow" />
        </q-toolbar>
      </q-header>
      <q-page-container>
        <grid-container>
          <div class="item" v-for="(thing, index) in getThingsList" :key="thing.uuid">
            <thing :thing="thing" :index="index"></thing>
          </div>
        </grid-container>
       
      </q-page-container>
    </q-layout>
  </div>
  <div v-else-if="$q.platform.is.mobile">
    <div v-for="(thing, index) in getThingsList" :key="thing.uuid">
      <thing :thing="thing" :index="index" />
    </div>
  </div>
</template>

<script>
import Thing from "./Thing.vue";
import GridContainer from "./common/GridContainer.vue";

export default {
  components: {
    Thing,
    GridContainer
  },
  computed: {
    getThingsList: function() {
      return this.$store.state.thingsList;
    }
  },
  data() {
    return {
      thingsDetail: false
    };
  },
  methods: {
    closeWindow: function() {
      this.$store.commit("closeSection");
    }
  }
};
</script>

<style scoped>
.current-section {
  position: fixed;
  top: 1%;
  bottom: 1%;
  left: 1%;
  right: 1%;
  background: transparent;
  border-radius: 4px;
  z-index: 130;
  color: black;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  overflow-y: auto;
  margin: auto;
}

#action-container {
  text-align: center;
  cursor: pointer;
  background-color: transparent;
  margin-top: 50%;
}

.small-icon {
  width: 24px;
  margin: 1%;
  cursor: pointer;
  background: transparent;
}
</style>

<template>
  <div id="app">
    <div id="navigation">
      <div id="navi-title">JittorVis</div>
    </div>
    <div id="content">
      <div id="left">
        <div id="statistic-container">
          <span>—— Statistic ——</span>
          <statistic></statistic>
        </div>
        <div id="navi-container">
          <span>—— Navigation ——</span>
          <navigation v-bind:canFocusNode="true"></navigation>
        </div>
        <div id="featuremap-container">
            <span>—— Features ——</span>
            <vue-scroll :ops="scrollOptions">
              <feature-map></feature-map>
            </vue-scroll>
        </div>
      </div>
      <div id="tree-container">
          <div id="network-container"><network></network></div>
      </div>
    </div>
  </div>
</template>

<script>
import Navigation from './components/Navigation.vue';
import Network from './components/Network.vue';
import Statistic from './components/Statistic.vue';
import FeatureMap from './components/FeatureMap.vue';
import axios from 'axios';

// main vue component
export default {
    components: {Network, Navigation, Statistic, FeatureMap},
    name: 'App',
    mounted: function() {
        const store = this.$store;
        axios.get(store.getters.URL_GET_ALL_DATA)
            .then(function(response) {
                store.commit('setAllData', response.data);
                console.log('network data', store.getters.network);
            });
    },
    data: function() {
        return {
            scrollOptions: {
                bar: {
                    background: '#c6bebe',
                },
            },
        };
    },
};
</script>

<style>
html, body, #app {
  margin: 0;
  width: 100%;
  height: 100%;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  display: flex;
  flex-direction: column;
}

#navigation {
  width: 100%;
  height: 50px;
  display: flex;
  align-items: center;
  background: rgb(54, 54, 54);
}

#navi-title {
  color: rgb(255, 255, 255);
  font-weight: 900;
  font-size: 40px;
  margin: 0 0 0 20px;
}

#statistic-container {
  width: 100%;
  height: 25%;
}

#tree-container {
  width: 70%;
  height: 100%;
  display: flex;
  overflow: hidden;
  margin-left: 3px;
  border-left: 1px solid lightgray;
}

#navi-container {
  width: 100%;
  height: 25%;
}

#featuremap-container {
  width: 100%;
  height: 50%;
}

#content {
  width: 100%;
  height: 100%;
  overflow: hidden;
  display: flex;
}

#left {
  width: 20%;
  height: 100%;
}

#network-container {
  width: 100%;
  height: 100%;
}

#statistic-container, #navi-container, #featuremap-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

#statistic-container > span, #navi-container > span, #featuremap-container > span {
  font-family: Lucida Sans Typewriter;
  font-weight: 400;
  margin: 5px 0 5px 0;
}

</style>

<template>
  <div class="maps">
    <breadcrumb :breadcrumb="breadcrumb" :title="title" />
    <page-hero>
      <h1>Maps</h1>
      <div class="sideText">
        Interactive maps reveal the anatomy and functional
        relationships of the autonomic nerves and the organs that they
        innervate. 2D and 3D maps render spatial dynamics, connectivity, and
        physiology across a range of species and nerve-organ systems.
      </div>
      <div class="sideTextRight">
        THESE PAGES ARE UNDER CONSTRUCTION<br>
        Currently only curated SPARC data are shown.<br>
        Please use ? for context-dependent help
      </div>
    </page-hero>
    <div class="page-wrap portalmapcontainer" ref="mappage">
      <client-only placeholder="Loading...">
        <div class="map-app">
          <MapContent />
        </div>
      </client-only>
    </div>
  </div>
</template>

<script>
import Breadcrumb from "@/components/Breadcrumb/Breadcrumb.vue";
import PageHero from "@/components/PageHero/PageHero.vue";
//Only available on the client side.
process.client
  ? import("@abi-software/mapintegratedvuer/dist/mapintegratedvuer.css")
  : null;

export default {
  name: "Maps",

  components: {
    Breadcrumb,
    PageHero,
    MapContent: process.client
      ? () => import("@/components/MapApp/MapApp")
      : null
  },

  data() {
    return {
      resources: [],
      title: "Maps",
      breadcrumb: [
        {
          to: {
            name: "index"
          },
          label: "Home"
        }
      ]
    };
  },

  methods: {}
};
</script>

<style lang="scss" scoped>
@import "@/assets/_variables.scss";
.maps {
  .sideText {
    top: 0px;
    font-size: 0.8em;
    position: absolute;
    line-height: 1.2em;
    width: 40em;
    margin-left: 6em;
  }

  .sideTextRight {
    top: 0px;
    padding-left: 8px;
    background-color: lightblue;
    color: black;
    font-size: 0.7em;
    position: absolute;
    line-height: 1.2em;
    left: 57em;
    width: 23em;
    text-align:center;
  }

  .portalmapcontainer {
    margin-top: 1.5rem;
    height: 90vh;
    max-width: calc(100% - 48px);
    padding-left: 24px;
  }

  .map-app {
    position: relative;
    width: 100%;
    height: 100%;
    border: solid 1px #dcdfe6;
    box-shadow: 0 1px 8px 0 rgba(0, 0, 0, 0.06);
  }
  .page-wrap {
    &__results {
      font-size: 0.875em;
      font-weight: normal;
      line-height: 1em;

      @media screen and (max-width: 768px) {
        margin-left: 0.9375rem;
      }

      p {
        margin-top: 1.5rem;
      }
    }
    @media (min-width: 48em) {
      padding-top: 0;
    }
  }
}
</style>
<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />
      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">Todo</div>
        <div class="text-subtitle1">{{ toDaysDate }}</div>
      </div>
      <q-img
        src="https://cdn.pixabay.com/photo/2016/11/18/19/37/conifers-1836582_640.jpg"
        class="header-image absolute-top"
      />
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :width="250"
      :breakpoint="600"
    >
      <q-scroll-area
        style="
          height: calc(100% - 192px);
          margin-top: 192px;
          border-right: 1px solid #ddd;
        "
      >
        <q-list padding>
          <q-item to="/" 
          exact
          clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="list" />
            </q-item-section>

            <q-item-section> Todo </q-item-section>
          </q-item>
          <q-item to="/help" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section> Help </q-item-section>
          </q-item>
          <q-item to="/settings" exact   clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="settings" />
            </q-item-section>

            <q-item-section> Setting </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>

      <q-img
        class="absolute-top"
        src="https://cdn.pixabay.com/photo/2016/11/18/19/37/conifers-1836582_640.jpg"
        style="height: 192px"
      >
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img
              src="https://cdn.pixabay.com/photo/2017/04/06/19/34/girl-2209147_960_720.jpg"
            />
          </q-avatar>
          <div class="text-weight-bold">Maddie Siegel</div>
          <div>@maddie_siegel</div>
          <div></div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from "quasar";
import EssentialLink from "components/EssentialLink.vue";

export default {
  name: "MainLayout",
  components: { EssentialLink },
  data() {
    return {
      leftDrawerOpen: false,
      essentialLinks: linksData,
    };
  },
  computed: {
    toDaysDate() {
      let timeStamp = Date.now();
      return date.formatDate(timeStamp, "DD MMMM YYYY");
    },
  },
};
</script>
<style lang="scss">
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 0.5;
  // filter: grayscale(100%);
}
</style>
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
          @click="drawer = !drawer"
        />
      </q-toolbar>
      <div>
        <div class="q-px-lg q-pt-xl q-pb-md">
          <div class="text-h3">Todo</div>
          <div class="text-subtitle1">{{ todaysDate }}</div>
        </div>
      </div>
      <q-img src="~assets/img/clouds.jpg" class="header-image absolute-top" />
    </q-header>

    <q-drawer v-model="drawer" show-if-above :width="200" :breakpoint="600">
      <q-scroll-area
        style="
          height: calc(100% - 150px);
          margin-top: 150px;
          border-right: 1px solid #ddd;
        "
      >
        <q-list padding>
          <q-item to="/" clickable v-ripple exact>
            <q-item-section avatar>
              <q-icon name="list" />
            </q-item-section>

            <q-item-section> To do </q-item-section>
          </q-item>

          <q-item to="/help" clickable v-ripple exact>
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section> Help </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>

      <q-img
        class="absolute-top"
        src="~assets/img/clouds.jpg"
        style="height: 150px"
      >
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="~assets/img/ikmal.jpg" />
          </q-avatar>
          <div class="text-weight-bold">Ikmal Shahzan</div>
          <div>@ishahzan</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <router-view v-slot="{ Component }">
        <keep-alive>
          <component :is="Component" />
        </keep-alive>
      </router-view>
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import { date } from "quasar";

export default defineComponent({
  name: "MainLayout",

  computed: {
    todaysDate() {
      let timeStamp = Date.now();
      return date.formatDate(timeStamp, "dddd D MMMM");
    },
  },

  setup() {
    return {
      drawer: ref(false),
    };
  },
});
</script>

<style lang="scss">
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 0.2;
  filter: grayscale(100%);
}
</style>

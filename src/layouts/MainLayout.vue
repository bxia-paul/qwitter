<template>
  <q-layout view="lHr lpR fFf">
    <q-header bordered class="bg-white text-grey-10">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title class="text-weight-bolder"> 
          <span class="gt-sm"> {{$route.name}} </span>
          <q-icon name="fas fa-dove" color="primary" size="sm" class="header-icon q-pl-xl lt-md " />
          </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <!-- left side -->
    <q-drawer
      show-if-above
      v-model="leftDrawerOpen"
      side="left"
      bordered
      :width="200"
    >
      
      <q-list class="column items-end q-py-md">
        <q-item clickable v-ripple to="/">
          <q-item-section avatar>
            <q-icon color="primary" name="fas fa-dove" size="md" />
          </q-item-section>
        </q-item>
      </q-list>

      <q-list class="column items-end">
        <q-item clickable v-ripple to="/">
          <q-item-section avatar>
            <q-icon color="primary" name="house" size="md" />
          </q-item-section>
        </q-item>
      </q-list>

      <q-list class="column items-end">
        <q-item clickable v-ripple to="/">
          <q-item-section avatar>
            <q-icon color="primary" name="explore" size="md" />
          </q-item-section>
        </q-item>
      </q-list>

      <q-list class="column items-end">
        <q-item clickable v-ripple to="/">
          <q-item-section avatar>
            <q-icon color="primary" name="notifications" size="md" />
          </q-item-section>
        </q-item>
      </q-list>

      <q-list class="column items-end">
        <q-item clickable v-ripple to="/">
          <q-item-section avatar>
            <q-icon color="primary" name="mail" size="md" />
          </q-item-section>
        </q-item>
      </q-list>

      <q-list class="column items-end">
        <q-item clickable v-ripple to="/profile">
          <q-item-section avatar>
            <q-icon color="primary" name="person" size="md" />
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <!-- right side -->
    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <!-- Search bar -->
      <q-input
        color="blue"
        standout
        bottom-slots
        v-model="text"
        label="Search"
        counter
        clearable
        class="q-ma-md"
        rounded
        dense
      >
        <template v-slot:prepend>
          <q-icon name="search" />
        </template>
      </q-input>

      <q-list padding>
        <q-item>
          <q-item-section>
            <q-item-label overline class="text-weight-bolder"
              >Trends for you</q-item-label
            >
            <q-item-label> U.W.I </q-item-label>
            <q-item-label caption
              >New professional promotions at U.W.I
            </q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
          </q-item-section>
        </q-item>

        <q-separator spaced />
      </q-list>

      <q-list padding>
        <q-item>
          <q-item-section>
            <q-item-label> Trinidad </q-item-label>
            <q-item-label caption
              >Medical drug supply shortage hits Trinidad and Tobago
            </q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
          </q-item-section>
        </q-item>

        <q-separator spaced />
      </q-list>

      <q-list padding>
        <q-item>
          <q-item-section>
            <q-item-label> COVID-19 </q-item-label>
            <q-item-label caption
              > new strain of Covid-19 exists that combines characteristics of the delta and omicron variants.
            </q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
          </q-item-section>
        </q-item>

        <q-separator spaced />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const leftDrawerOpen = ref(false);
    const rightDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },

      rightDrawerOpen,
      toggleRightDrawer() {
        rightDrawerOpen.value = !rightDrawerOpen.value;
      },
    };
  },
};
</script>

<style lang="css">
.header-icon{
  position: relative;
  bottom: 0;
  left: 40%;
  transform: translateX(-50%);
}
</style>

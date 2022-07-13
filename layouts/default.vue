<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app>
      <div class="logo py-4 d-flex justify-center mx-16">
        <NuxtLogo />
      </div>
      <v-list>
        <v-list-group
          v-for="item in items"
          :key="item.title"
          v-model="item.active"
          :prepend-icon="item.action"
          no-action
        >
          <template v-slot:activator>
            <v-list-item-content>
              <v-list-item-title v-text="item.title"></v-list-item-title>
            </v-list-item-content>
          </template>

          <v-list-item v-for="child in item.items" :key="child.title">
            <v-list-item-content>
              <v-list-item-title v-text="child.title"></v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-group>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-row class="mt-1">
        <v-col cols="4">
          <v-text-field label="Search products"></v-text-field>
        </v-col>
        <v-col cols="4"></v-col>
        <v-col cols="2">
          <v-select
            v-model="select"
            :items="languages"
            item-text="name"
            item-value="code"
            label="Select"
            return-object
            single-line
          ></v-select>
        </v-col>
        <v-col cols="2">
          <v-badge color="green" content="0" class="mt-2">
            <v-icon aria-hidden="false"> mdi-cart </v-icon>
          </v-badge>
        </v-col>
      </v-row>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {
      clipped: false,
      drawer: false,
      select: { name: "English", code: "EN" },
      languages: [
        { name: "English", code: "EN" },
        { name: "French", code: "FR" },
        { name: "German", code: "DE" },
      ],
      items: [
        {
          action: "mdi-ticket",
          items: [{ title: "List Item" }],
          title: "Menu 1",
        },
        {
          action: "mdi-silverware-fork-knife",
          active: true,
          items: [
            { title: "Breakfast & brunch" },
            { title: "New American" },
            { title: "Sushi" },
          ],
          title: "Menu 2",
        },
        {
          action: "mdi-school",
          items: [{ title: "List Item" }],
          title: "Menu 3",
        },
        {
          action: "mdi-human-male-female-child",
          items: [{ title: "List Item" }],
          title: "Menu 4",
        },
        {
          action: "mdi-bottle-tonic-plus",
          items: [{ title: "List Item" }],
          title: "Menu 5",
        },
        {
          action: "mdi-briefcase",
          items: [{ title: "List Item" }],
          title: "Menu 6",
        },
        {
          action: "mdi-tag",
          items: [{ title: "List Item" }],
          title: "Menu 7",
        },
      ],
    };
  },
};
</script>

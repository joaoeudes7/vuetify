<template>
  <v-row>
    <v-col
      v-for="(bar, i) in bars"
      :key="i"
      cols="12"
      sm="12"
      md="6"
      class="my-4"
    >
      <v-card color="grey lighten-4" flat height="200px">
        <v-toolbar :color="bar.class" :dark="bar.dark">
          <v-app-bar-nav-icon></v-app-bar-nav-icon>
          <v-toolbar-title>Title</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn icon>
            <v-icon>search</v-icon>
          </v-btn>
          <v-btn icon>
            <v-icon>favorite</v-icon>
          </v-btn>
          <v-btn icon>
            <v-icon>more_vert</v-icon>
          </v-btn>
        </v-toolbar>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
  export default {
    data: () => ({
      bars: [
        { class: '' },
        { class: '', dark: true },
        { class: 'primary', dark: true },
        { class: 'elevation-0' },
      ],
    }),
  }
</script>

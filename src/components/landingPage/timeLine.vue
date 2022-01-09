<template>
  <v-container>
    <v-toolbar flat>
      <v-toolbar-title>TimeLine</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-tooltip bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn v-if="isOverView" v-bind="attrs" v-on="on" icon @click.stop="lastPage"><v-icon>mdi-chevron-double-up</v-icon></v-btn>
        </template>
        <span>Last Page</span>
      </v-tooltip>
      <v-tooltip bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn v-if="isOverView" v-bind="attrs" v-on="on" icon @click.stop="nextPage"><v-icon>mdi-chevron-double-down</v-icon></v-btn>
        </template>
        <span>Next Page</span>
      </v-tooltip>
    </v-toolbar>

    <vue-horizontal-timeline class="d-md-none" :items="horizontalItems" />

    <v-timeline class="d-none d-md-block">
      <v-timeline-item
          v-for="timeLine in timeLines"
          :key="timeLine.id"
          color="#ff9900"
          large
      >
        <template v-slot:opposite>
          <span>{{ timeLine.time }}</span>
        </template>
        <v-card class="elevation-2">
          <v-card-title class="headline">{{ timeLine.title }}</v-card-title>
          <v-card-text>{{timeLine.content}}</v-card-text>
        </v-card>
      </v-timeline-item>
    </v-timeline>
  </v-container>
</template>

<script>
import { VueHorizontalTimeline } from "vue-horizontal-timeline";
export default {
name: "timeLine",
  props: {
    value: Boolean,
    isOverView: {
      default: false,
      type: Boolean
    }
  },
  components: {
    VueHorizontalTimeline,
  },
  data(){
    return {
      timeLines: [
        {time: "22 January 2022 - 23 January 2022", title: "Workshop", content: "Workshops will be held, ensuring participants have better preparation for the competition."},
        {time: "22 January 2022", title: "Briefing Session", content: "Briefing session will be held to help participants to have better understanding about the competition."},
        {time: "29 January 2021 - 30 January 2021", title: "CityHack22", content: "Let’s start Hacking for 24 hours!"},
      ],
      horizontalItems: [
        {title: "22-23 Jan. 2022", content: "Workshops will be held, ensuring participants have better preparation for the competition."},
        {title: "22 Jan. 2022", content: "Briefing session will be held to help participants to have better understanding about the competition."},
        {title: "29-30 Jan. 2022", content: "Let’s start Hacking for 24 hours!"}
      ]
    }
  },
  computed: {
    show: {
      get () {
        return this.value
      },
      set (value) {
        this.$emit('input', value)
      }
    }
  },
  methods: {
    nextPage() {
      this.$emit('next');
    },
    lastPage() {
      this.$emit('last');
    }
  }
}
</script>

<style scoped>
.v-timeline:before {
  left: 50%;
}
</style>

<template>
  <div id="app">
    <vue-inline-calendar @select-date="setDate" enable-mousewheel-scroll />
  </div>
  <div
    style="display: grid; justify-content: center; justify-items: center"
  ></div>
  <planner :placeName="placeNameChanged" />
</template>

<script>
import { getAuth, onAuthStateChanged } from "firebase/auth";
import planner from "../components/Planning.vue";
import Map from "../components/Map.vue";
import { ref } from "vue";
import VueInlineCalendar from "vue-inline-calendar";

export default {
  name: "Plan",
  data() {
    return {
      placeName: "",
    };
  },
  components: {
    planner,
    Map,
    VueInlineCalendar,
  },
  created() {
    const auth = getAuth();
    onAuthStateChanged(auth, (user) => {
      if (!user) {
        this.$router.push("/login").catch(() => {});
      }
    });
  },
  setup() {
    const selectedDate = ref(null);

    return {
      selectedDate,
    };
  },
};
</script>

<style >
.inline-calendar[data-v-de945bb6] {
  display: flex;
  margin-bottom: 8px;
  padding: 0 10px;
  padding-bottom: 10px
}
.inline-calendar__dates[data-v-de945bb6] {
  display: grid;
  grid-auto-flow: column;
  margin-left: -10px;
  margin-right: -10px;
  padding: 8px 10px;
  list-style-type: none;
  overflow-x: scroll;
  white-space: nowrap;
  -ms-overflow-style: none;
  scrollbar-width: none;
}
.inline-calendar__dates[data-v-de945bb6]::-webkit-scrollbar {
  display: none;
  
}
.inline-calendar__date[data-v-de945bb6] {
  padding: 14px;
  background-image: linear-gradient(to top, #ff83a8, #ff8f8f);
  border: 1px solid #ffffff;
  border-radius: 8px;
  cursor: pointer;
  
}
.inline-calendar__date.today[data-v-de945bb6] {
  color: #ffffff;
  border-color: #000000;
  background-image: linear-gradient(to top, #cc2e5d, #ff5858);
  
}
.inline-calendar__date.in-range[data-v-de945bb6] {
  color: #fff;
  border-color: #0094ff99 !important;
  background-color: #000000 !important;
  
}
.inline-calendar__date.active[data-v-de945bb6] {
  color: #fff;
  border-color: #000000 !important;
  background-image: linear-gradient(to top, #cc2e5d, #ff5858);
}
.inline-calendar__date.disabled[data-v-de945bb6] {
  opacity: 0.4;
  pointer-events: none;
}

.date-item__month,
.date-item__weekday {
  font-size: 12px;
  line-height: 14px;
  color: rgb(255, 255, 255); /* เปลี่ยนสีข้อความในนี้เป็นสีขาว */
}

/* .date-item__month */
.date-item__month {
  margin: 0 0 8px;
}

/* .date-item__weekday */
.date-item__weekday {
  font-weight: 500;
}

/* .date-item__day */
.date-item__day {
  margin: 10px 0;
  font-weight: 600;
  font-size: 16px;
  line-height: 18px;
  color: #ffffff; /* เปลี่ยนสีข้อความในนี้เป็นสีขาว */
}

/* .date-item__year */
.date-item__year {
  margin: 0 0 8px;
  font-size: 12px;
  font-weight: 500;
  line-height: 14px;
  color: #ffffff; /* เปลี่ยนสีข้อความในนี้เป็นสีขาว */
}
</style>

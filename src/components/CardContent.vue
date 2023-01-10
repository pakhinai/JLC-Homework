<template>
  <div class="bgColor">
    <div class="container py-3">
      <span>You curren timezone is Asia/Bangkok</span>

      <b-card
        v-for="(item, index) in dataFilter"
        :key="index"
        class="mb-2 mt-2"
      >
        <b-container>
          <div class="d-flex flex-column flex-sm-row align-items-sm-center">
            <div class="d-flex align-items-center">
              <b-avatar
                variant="info"
                :src="item.dataFind.avatar_url"
                class="mr10px"
              ></b-avatar>

              <p class="textOrange mr10px">{{ item.dataFind.name }}</p>
            </div>
            <p class="mt-2 mt-sm-0">
              posted on {{ changeString(item.created_at) }}
            </p>
          </div>
        </b-container>

        <hr class="solid" />

        <b-container>
          <b-row offset="5">
            <b-col cols="12" md="4">
              <b-img
                :src="item.image_url"
                fluid
                alt="Fluid image"
                class="w-100 cursor"
              ></b-img>
            </b-col>

            <b-col cols="12" md="8" class="mt-3 mt-md-0">
              <h4 class="cursor">{{ item.title }}</h4>
              <p>{{ item.body }}</p>
            </b-col>
          </b-row>
        </b-container>
      </b-card>
    </div>
  </div>
</template>

<script>
import AuthorsJson from "../assets/dataJson/authors.json";
import PostJson from "../assets/dataJson/posts.json";
export default {
  name: "CardContent",

  computed: {
    dataFilter() {
      const data = PostJson.map((item) => {
        const dataFind = AuthorsJson.find(
          (element) => element.id === item.author_id
        );
        return {
          ...item,
          dataFind,
        };
      });

      return data;
    },
  },

  methods: {
    changeString(val) {
      const days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      const months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      const date = new Date(val);
      const dateString = date.toString().split(" ");
      const day = date.getDay();
      const month = date.getMonth();

      let text = `${days[day]}, ${months[month]} ${dateString[2]}, ${
        dateString[3]
      }, ${dateString[4].slice(0, 5)}`;
      return text;
    },
  },
};
</script>

<style scoped>
.bgColor {
  background: #eeeeee;
}
.textOrange {
  color: #e2512d;
}
.mr10px {
  margin-right: 10px;
}
.cursor {
  cursor: pointer;
}
p {
  margin: 0;
}
</style>
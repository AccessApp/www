<template>
  <div class="ambasadors">
    <figure-circle
      color="#F7F7FA"
      :zIndex="0"
      :left="-200"
      :isFilled="false"
      :bottom="0"
    ></figure-circle>
    <div class="container">
      <div class="row">
        <div class="col-12">
          <h2>{{ title }}</h2>
        </div>
      </div>
      <div class="row content">
        <div
          class="col-xl-4 col-md-12 col-xs-4 col-12"
          v-for="person of people"
          :key="person.name"
        >
          <img :src="person['avatar-link']" class="person-avatar" />
          <h3 class="person-name">{{ person.name }}</h3>
          <p class="person-place">{{ person.place }}</p>
          <p class="person-description">{{ person.description }}</p>

          <div
            v-if="person.email || person.number || person.twiter || person.linkedin"
            class="lines"
          />
          <div class="contacts">
            <div class="center">
              <div class="row" v-if="person.email">
                <img  src="/assets/team-email.svg" />
                <p>
                  <a :href="`mailto:${person.email} `">{{ person.email }}</a>
                </p>
              </div>
              <div class="row" v-if="person.number">
                <img src="/assets/team-number.svg" />
                <p>{{ person.number }}</p>
              </div>
              <div class="row" v-if="person.twitter">
                <img src="/assets/team-twitter.svg" />
                <a :href="person.twitter" target="_blank"
                  ><p>{{ person.twitter }}</p></a
                >
              </div>
              <div class="row" v-if="person.linkedin">
                <img  src="/assets/team-linkedin.svg" />
                <a :href="person.linkedin" target="_blank"
                  ><p>{{ person.linkedin }}</p></a
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ambasadors from "@content/en/ambasadors.yaml";
import ambasadorsDe from "@content/de/ambasadors.yaml";
import FigureCircle from "../components/FigureCircle.vue";
export default {
  name: "ambasadors",
  components: {
    FigureCircle,
  },
  data() {
    return {
      title: "",
      people: [],
      place: "",
    };
  },
  watch: {
    $route() {
      this.init();
    },
  },
  mounted() {
    this.init();
  },
  methods: {
    init() {
      const data =
        this.$router.history.current.params.lang == "en" ? ambasadors : ambasadorsDe;
      this.title  = data.title;
      this.people = data.people;
      this.place  = data.organisation;
    },
  },
};
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Rubik:wght@500&display=swap");
@import "../../public/assets/scss/main.scss";
.person-description {
  font-family: $font__descriptions;
  font-size: 18px;
  color: #9597ac;
  width: 75%;
  margin: 0 auto;
  margin-bottom: 0px;
  height: 9.5rem;
}

.ambasadors {
  display: none;
  position: relative;
  margin-top: -6rem;
  .container {
    margin-top: 100px;
  }
}
.col-12 {
  font-family: $font__family;
  font-size: 40px;
  margin-bottom: 50px;
  color: #1e2f67;
}
.person-name {
  font-family: $font__family;
  font-size: 25px;
  color: #385fe2;
  margin-top: 60px;
}
.person-place {
  font-family: "Rubik", sans-serif;
  font-size: 16px;
  color: #9597ac;
  padding-bottom: 0px;
  font-weight: 500;
}
.lines {
  width: 175px;
  border-bottom: 1px solid #dbddeb;
  margin: 35px auto 0;
}
.content {
  margin-top: 35px;
}
.contacts {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  .center {
    margin: 0 auto;
    .row {
      justify-content: flex-start;
      align-items: end;
      flex-wrap: unset;
    }
    a{
      margin-top: 5px;
    }
    p {
      font-size: 12px;
      color: #1e2f67;
      font-weight: 400;
    }
    img {
      margin-right: 10px;
    }
  }
}
@media only screen and (max-width: 768px) {
  .person-avatar {
    margin-top: 50px;
    max-width: 140px;
    max-height: 140px;
  }
  .ambasadors .content {
    margin-top: 0;
  }
}
@media only screen and (max-width: 993px) {
  .content {
    flex-direction: column;
  }
  .person-description {
    height: fit-content;
  }
}
</style>
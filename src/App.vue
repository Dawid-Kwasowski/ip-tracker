<template>
  <div class="container-fluid">
    <div class="row">
      <div class="header">
        <h1 class="text-center text-white m-3">IP TRACKER 🕵️</h1>
        <div class="input-group input-group-lg mt-5">
          <input
            type="text"
            class="form-control"
            v-model="ipAddress"
            :placeholder="ipAddress"
            @change="sendQuery"
            @click.enter="sendQuery"
            required
          />
        </div>
      </div>
      <div class="card">
        <LocationInfo :ipAddress="ipAddress" :isp="isp" :country="country" :city="city" />
      </div>
    </div>
    <div class="row">
      <div class="col-sm-6" v-for="question in questions" :key="question.name">
        <QuickInfo>
          <template #card-title>
            <h4>{{ question.name }}</h4>
          </template>
          <template #card-text>
            <p>{{ question.description }}</p>
            <a :href="question.definitionAddress">➡️Zobacz więcej</a>
          </template>
        </QuickInfo>
      </div>
    </div>
  </div>
</template>

<script>
import LocationInfo from "./components/LocationInfo";
import QuickInfo from "./components/QuickInfo.vue";
export default {
  name: "App",
  components: {
    LocationInfo,
    QuickInfo,
  },
  data() {
    return {
      isError: true,
      ipAddress: "",
      isp: "",
      country: "",
      city: "",
      apiKey: "apiKey=at_TbgRReQumb7ampURA6ms5j1bg9T2h",
      apiUrl: "https://geo.ipify.org/api/v1?",

      questions: [
        {
          name: "Czym adress IP 📯",
          description:
            "Adres IP pozwala komputerowi łączyć się z innymi urządzeniami przez Internet. Umożliwia rozpoznanie systemu przez inne systemy połączone za pomocą protokołu internetowego. Adres IP pozwala internetowi znaleźć konkretne urządzenie wśród miliardów innych podłączonych do niego urządzeń. To ekwiwalent kodu pocztowego, ulicy i numeru domu w internecie.",
          definitionAddress: "https://harbingers.io/definicje/adres-ip",
        },
        {
          name: "ISP (Internet Service Provider) 🌐",
          description:
            "ISP albo inaczej dostawca dostępu do internetu, to, mówiąc prościej, firma, która zapewnia dostęp do sieci osobom fizycznym i podmiotom gospodarczym.",
          definitionAddress: "https://harbingers.io/definicje/isp",
        },
      ],
    };
  },
  created() {
    this.query(`${this.apiUrl}${this.apiKey}`);
  },

  methods: {
    sendQuery() {
      return this.query(`${this.apiUrl}${this.apiKey}&ipAddress=${this.ipAddress}`);
    },

    query(apiUrl) {
      return fetch(apiUrl)
        .then((response) => response.json())
        .then((parsedData) => {
          this.ipAddress = parsedData.ip;
          this.isp = parsedData.isp;
          this.country = parsedData.location.country;
          this.city = parsedData.location.city;
        })
        .catch((error) => console.error(`Error: ${error}`));
    },
  },
};
</script>

<style lang="scss">
body {
  background: #eee;
}
.header {
  background-image: url("../src/assets/images/pattern-bg.png");
  width: 100%;
  height: 200px;
}
</style>

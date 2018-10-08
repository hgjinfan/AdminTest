<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <div class="connect" @click="connect">connectBtn</div>
    <div v-text="status"></div>
    <ul>
      <li v-for='(log, index) in list' v-text='log.data' :key='index'></li>
    </ul>
    <input type="text" v-model='log'> <span @click='sendMessage(log)'>sendBtn</span>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "home",
  data() {
    return {
      websoket: null,
      wsUrl: "wss://echo.websocket.org/",
      list: [],
      status: "close",
      log: ""
    };
  },
  components: {
    HelloWorld
  },
  methods: {
    connect() {
      this.websoket = new WebSocket(this.wsUrl);
      this.status = "connect..."
      this.websoket.onopen = () => {
        this.status = "connected"
      }
      this.websoket.onclose = () => {
        this.status = 'close'
      }
      this.websoket.onmessage = (e) => {
        this.list.push(e)
      }
    },
    sendMessage(text) {
      this.websoket.send(text)
    }
  },
  created() {
    this.$http
      .get("/hello.json")
      .then(response => {
        // eslint-disable-next-line
        console.log(response);
      })
      .catch(erro => {
        // eslint-disable-next-line
        console.error(erro);
      });
    this.$http
      .post("http://api.xiaojumuying.com/mobile/Index/getStaffList", {
        type: "月嫂",
        name: "",
        age: ["50~60"],
        workYears: "",
        education: [],
        province: "",
        page: 1
      })
      .then(function(response) {
        // eslint-disable-next-line
        console.log(response);
      });
  }
};
</script>

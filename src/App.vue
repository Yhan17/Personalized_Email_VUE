<template>
  <div id="app">
    <h1>Email</h1>
    <label>Assunto</label><br />
    <input v-model="subject" /><br />
    <label>Para quem</label><br />
    <input v-model="toEmail" />
    <vue-editor v-model="html"></vue-editor>
    <div class="button">
      <button @click="submit">Email</button>
    </div>
  </div>
</template>

<script>
import { VueEditor } from "vue2-editor";
const url = process.env.VUE_APP_API_BASE_URL;
import axios from "axios";

export default {
  name: "App",
  components: {
    VueEditor,
  },
  data() {
    return {
      html: "",
      toEmail: "",
      subject: "",
    };
  },
  methods: {
    submit: function () {
      console.log(this.html);
      axios
        .post(
          `${url}/sendemail`,
          {
            html: this.html,
            toEmail: this.toEmail,
            subject: this.subject,
          },
          {
            headers: {
              "Access-Control-Allow-Origin": "*",
            },
          }
        )
        .then((res) => {
          console.log(res);
        })
        .catch((err) => {
          console.log(err.response);
        });
    },
  },
};
</script>

<style>
h1 {
  text-align: center;
}
.button {
  display: flex;
  justify-content: flex-end;
}

.button button {
  border: none;
  margin: 0;
  padding: 0;
  width: auto;
  overflow: visible;

  background: transparent;

  /* inherit font & color from ancestor */
  color: inherit;
  font: inherit;

  /* Normalize `line-height`. Cannot be changed from `normal` in Firefox 4+. */
  line-height: normal;

  /* Corrects font smoothing for webkit */
  -webkit-font-smoothing: inherit;
  -moz-osx-font-smoothing: inherit;

  /* Corrects inability to style clickable `input` types in iOS */
  -webkit-appearance: none;
  background-color: rgb(65, 90, 201);
  color: white;
  padding: 7px;
  padding-left: 15px;
  padding-right: 15px;
  margin-top: 10px;
  border-radius: 3px;
  border: 1px solid rgb(65, 90, 201);
  cursor: pointer;
}

.button button:hover {
  transition: 0.2s;
  margin-top: 8px;
}
</style>

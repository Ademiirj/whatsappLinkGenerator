<template>
  <div id="app">
    <div class="container">
      <div class="row justify-content-md-center">
        <div class="title-main">
          <h3 class="title text-success">Gerador de Whatsapp link</h3>
          <div class="title-image">
            <img
              class="img-logo"
              src="https://www.shapeweb.com.br/blog/wp-content/uploads/2019/01/qrcode-shape-web-whatsapp-250x250.png"
            />
          </div>
        </div>
      </div>
      <form>
        <div class="row justify-content-md-center">
          <div class="col-lg-3">
            <the-mask
              class="form-control form-control-lg"
              :mask="['(##) ####-####', '(##) #####-####']"
              v-model="number"
            />
          </div>
          <div class="col-lg-7">
            <textarea
              class="form-control"
              rows="4"
              v-model="message"
              placeholder="Criar mensagem automática"
            ></textarea>
          </div>
        </div>
        <div class="border border-light p-3 mb-4">
          <div class="text-center">
            <button type="button" v-on:click="teste" class="ademir btn btn-primary">Gerar QrCode</button>
          </div>
        </div>
        <Result v-bind:link-whats = baseSendWhats v-bind:link-qr = baseURL></Result>
      </form>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import { TheMask } from "vue-the-mask";
import Result from "./components/Result.vue";

// import "font-awesome/dist/css/font-awesome.css";

export default {
  name: "App",
  components: { TheMask , Result},
  data() {
    return {
      baseURL: "https://chart.googleapis.com/chart?chs=150x150&cht=qr&chl=Acesse github.com/Ademiirj",
      baseSendWhats: "",
      number: "",
      message: "",
    };
  },
  methods: {
    teste() {
      this.variableReset();
      this.textFilter();
      this.baseSendWhats += this.number;
      this.baseSendWhats += "&text=" + this.message;
      this.baseURL += this.baseSendWhats;
    },
    textFilter() {
      this.message = this.message.replace(new RegExp(" ", "g"), "%20");
    },
    variableReset() {
      this.baseURL =
        "https://chart.googleapis.com/chart?chs=150x150&cht=qr&chl=";
      this.baseSendWhats = "https://api.whatsapp.com/send?phone=55";
    },
    copyText(){
      var vm = this
      /* Get the text field */
      var copyText = vm.$refs.input;
      /* Select the text field */
      copyText.select();
      /* Copy the text inside the text field */
      document.execCommand("copy");
      /* Alert the copied text */
      alert("Texto copiado com sucesso");
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 30px;
}
.ademir {
  padding: 15px;
  padding-left: 100px;
  padding-right: 100px;
}
.text-result{
  text-align: justify;
  white-space: normal
}
.title-main {
  display: grid;
  grid-template-columns: 3fr 1fr;
  margin: auto;
  position: relative;
  margin-bottom: 60px;
}
.title-image img {
  width: 4.7rem;
  float: left;
  padding: 5px;
  margin-top: 8px;
  margin-left: 24px;
}
.title {
  margin-top: 24px;
}
.testando{
  white-space:normal;
  overflow:hidden;
}
</style>

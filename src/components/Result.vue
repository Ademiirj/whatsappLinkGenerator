<template>
  <div id="app">
    <div class="testando border border-primary p-3 mb-4">
      <input
        type="text"
        ref="input"
        readonly
        class="text-currency form-control-plaintext"
        v-model="linkWhats"
      />
      <button type="button" v-on:click="copyText" class="ademir btn btn-primary">Copy</button>
    </div>

    <img v-bind:src="linkQr" />
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "vue-toast-notification/dist/theme-default.css";
import Vue from "vue";
import VueToast from "vue-toast-notification";

Vue.use(VueToast);

export default {
  name: "Result",
  props: ["linkWhats", "linkQr"],
  methods: {
    copyText() {
      var vm = this;
      /* Get the text field */
      var copyText = vm.$refs.input;
      /* Select the text field */
      copyText.select();
      /* Copy the text inside the text field */
      document.execCommand("copy");
      /* Alert the copied text */
      //   alert("Texto copiado com sucesso");
      Vue.$toast.open({
        message: "Texto copiado com sucesso",
        type: "success",
        position: "top-left",
        pauseOnHover: false,
      });
    },
  },
};
</script>

<style>
</style>

<template>
  <div :class="['footer-container', { 'dark-mode': nightMode }]">
    <div class="container py-3">
      <div class="row pt-1 align-items-center">
        <div class="col-xl-6 col-bg-6 col-md-6 col-sm-12 pbelow center-copyright">
          <span :class="{ 'text-light': nightMode, 'text-dark': !nightMode }">
            © 2024 Copyright: Valerie Celis
          </span>
        </div>
        <div class="col-xl-6 col-bg-6 col-md-6 col-sm-12">
          <div class="button-group">
            <button class="btn" :class="buttonClass" @click="open('facebook')">
              <i class="fab fa-facebook" :class="iconClass"></i>
            </button>
            <button class="btn" :class="buttonClass" @click="open('github')">
              <i class="fab fa-github" :class="iconClass"></i>
            </button>
            <button class="btn" :class="buttonClass" @click="open('telegram')">
              <i class="fab fa-telegram" :class="iconClass"></i>
            </button>
            <button class="btn" :class="buttonClass" @click="open('instagram')">
              <i class="fab fa-instagram" :class="iconClass"></i>
            </button>
            <button class="btn" :class="buttonClass" @click="open('resume')">
              <i class="fa fa-file" :class="iconClass"></i>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Footer",
  props: {
    nightMode: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    buttonClass() {
      return this.nightMode ? "btn-dark-mode" : "btn-light-mode";
    },
    iconClass() {
      return this.nightMode ? "text-light" : "text-dark";
    },
  },
  methods: {
    open(link) {
      window.open(this[link], "_blank");
    },
  },
};
</script>

<style scoped>
.button-group {
  display: flex;
  justify-content: center;
  gap: 10px; /* Adjust the value as needed */
}
.dark-mode {
  background-color: #121212;
  color: #d3d2d2;
}
.text-dark {
  color: black;
}
.text-light {
  color: #d3d2d2;
}
.btn-dark-mode {
  background-color: #3b3030;
  color: white;
  border-color: #3b3030;
}
.btn-dark-mode:hover {
  background-color: #795757;
  border-color: #795757;
  color: white;
}
.btn-light-mode {
  border-color: #3b3030;
  color: #759cc9;
}
.btn-light-mode:hover {
  background-color: #795757;
  border-color: #795757;
  color: white;
}
@media screen and (min-width: 360px) and (max-width: 480px) {
  .center-copyright {
    text-align: center !important;
  }
}
</style>

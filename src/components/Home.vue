<template>
  <div :class="{ 'bg-white': !nightMode, 'bg-dark': nightMode }" class="pt-5 p-st">
    <div
      class="container pb-5"
      data-aos="fade"
      data-aos-once="true"
      data-aos-duration="1000"
    >
      <div class="row align-items-center">
        <div class="col-xl-6 col-bg-6 col-md-6 col-sm-12 text-center">
          <div class="image">
            <img :src="picture" />
          </div>
        </div>
        <div class="col-xl-6 col-bg-6 col-md-6 col-sm-12 pt-5">
          <span
            class="home-title"
            :class="{ pgray: !nightMode, 'text-light': nightMode }"
          >
            <span ref="typewriterText"></span>
          </span>
          <div>
            <p v-html="description"></p>
          </div>
          <div class="text-center pb-4">
            <button
              class="btn mx-2"
              :class="nightMode ? 'btn-light' : 'btn-outline-secondary'"
              @click="open('facebook')"
              v-tooltip.bottom="'Facebook'"
            >
              <i :class="['fab fa-facebook', nightMode ? 'text-light' : 'text-dark']"></i>
            </button>
            <button
              class="btn mx-2"
              :class="nightMode ? 'btn-light' : 'btn-outline-secondary'"
              @click="open('github')"
              v-tooltip.bottom="'GitHub'"
            >
              <i :class="['fab fa-github', nightMode ? 'text-light' : 'text-dark']"></i>
            </button>
            <button
              class="btn mx-2"
              :class="nightMode ? 'btn-light' : 'btn-outline-secondary'"
              @click="open('telegram')"
              v-tooltip.bottom="'Telegram'"
            >
              <i :class="['fab fa-telegram', nightMode ? 'text-light' : 'text-dark']"></i>
            </button>
            <button
              class="btn mx-2"
              :class="nightMode ? 'btn-light' : 'btn-outline-secondary'"
              @click="open('instagram')"
              v-tooltip.bottom="'Instagram'"
            >
              <i
                :class="['fab fa-instagram', nightMode ? 'text-light' : 'text-dark']"
              ></i>
            </button>
            <button
              class="btn mx-2"
              :class="nightMode ? 'btn-light' : 'btn-outline-secondary'"
              @click="open('resume')"
              v-tooltip.bottom="'Resume'"
            >
              <i :class="['fa fa-file', nightMode ? 'text-light' : 'text-dark']"></i>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import info from "../../info";
import Wave from "./helpers/Wave";

export default {
  name: "Home",
  components: {
    Wave,
  },
  props: {
    nightMode: {
      type: Boolean,
    },
  },
  data() {
    return {
      picture: info.flat_picture,
      description: info.description,
      name: info.name,
      facebook: info.links.facebook,
      github: info.links.github,
      telegram: info.links.telegram,
      instagram: info.links.instagram,
      resume: info.links.resume,
      messages: ["Hi there!", "I'm Valerie"], // Array of messages
      typingSpeed: 100, // Speed of typing
      pauseDuration: 1000, // Pause duration after complete message
      currentIndex: 0, // Current index for typing
      currentMessageIndex: 0, // Index of the current message in the array
    };
  },
  mounted() {
    this.typeWriterEffect();
  },
  methods: {
    typeWriterEffect() {
      const typewriterText = this.$refs.typewriterText;
      const message = this.messages[this.currentMessageIndex]; // Get the current message
      this.currentIndex = 0; // Reset index for the new message

      const typeWriter = () => {
        if (this.currentIndex < message.length) {
          typewriterText.innerHTML = message.substring(0, this.currentIndex + 1);
          this.currentIndex++;
          setTimeout(typeWriter, this.typingSpeed);
        } else {
          // Start the pause duration after the message is fully typed
          setTimeout(() => {
            this.currentMessageIndex =
              (this.currentMessageIndex + 1) % this.messages.length; // Cycle through messages
            this.typeWriterEffect(); // Call the typeWriterEffect for the next message
          }, this.pauseDuration);
        }
      };

      typeWriter();
    },
    open(link) {
      switch (link) {
        case "facebook":
          window.open(this.facebook, "_blank");
          break;
        case "github":
          window.open(this.github, "_blank");
          break;
        case "telegram":
          window.open(this.telegram, "_blank");
          break;
        case "instagram":
          window.open(this.instagram, "_blank");
          break;
        case "resume":
          window.open(this.resume, "_blank");
          break;
      }
    },
  },
};
</script>
<style scoped>
.text-light {
  color: #ffffff; /* Light color for icons in dark mode */
}

.text-dark {
  color: #000000; /* Black color for icons in light mode */
}

.btn-light {
  background-color: #f8f9fa; /* Adjust color for light buttons */
  color: #000; /* Change text color for light buttons */
  border-color: #ced4da; /* Border color for light buttons */
}

.btn-outline-secondary {
  color: black; /* Adjusted color for the outline */
}

.text-light {
  color: black; /* Light color for text/icons in dark mode */
}

.home-title {
  font-size: 38px;
  font-weight: 800;
  color: #664343;
  white-space: nowrap;
  overflow: hidden;
  border-right: 3px solid; /* Cursor effect */
  width: fit-content;
  animation: blink-cursor 0.75s step-end infinite;
}

@keyframes blink-cursor {
  from,
  to {
    border-color: transparent;
  }
  50% {
    border-color: #664343;
  }
}

/* Floating effect for the image */
.image {
  margin: auto 0;
  width: 75%; /* Diameter of the circle */
  height: 75%; /* Diameter of the circle */
  border-radius: 50%; /* Make the image round */
  animation: imgFloat 7s ease-in-out infinite; /* Floating animation */
  overflow: hidden; /* Hide overflow to keep the image rounded */
}

.image img {
  width: 100%;
  height: 100%;
  object-fit: cover; /* Ensure the image fills the rounded container */
  object-position: center; /* Keep the center part visible */
}

@keyframes imgFloat {
  50% {
    transform: translateY(10px);
    border-radius: 45% 55% 45% 55%;

    /* Optional: change the border radius during floating */
  }
}

@media only screen and (max-width: 580px) {
  .image {
    width: 200px; /* Adjust the width for smaller screens */
    height: 200px; /* Adjust the height for smaller screens */
  }
}

.fa {
  font-size: 15px;
  color: black;
}
.fab {
  font-size: 15px;
  color: black;
}

.btn {
  border-color: black;
  color: #759cc9;
}

.btn:hover {
  background-color: #664343;
  border-color: #664343;
  color: white;
}

.btn:focus {
  background-color: #3b3030;
  border-color: #3b3030;
  color: white;
}

.btn:focus {
  outline: none !important;
}

p {
  text-align: justify;
  font-weight: 400;
}
@media (min-width: 360px) and (max-width: 480px) {
  .image {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0 auto; /* Center container horizontally */
  }

  .col-sm-12 {
    text-align: center; /* Ensure text inside is centered */
  }
}
</style>

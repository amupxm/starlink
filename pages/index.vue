<template lang="pug">
.app
  .min-h.row-container.container
    .row.w-100
      .col-md-6.text-box
        h1(v-html="addEmoji('🚀 ROCKET')")
        .row.text-box.p-5
          .col-md-8.col-sm-12
            p “The idea of lying on a beach as my main thing just sounds like the worst — it sounds horrible to me. I would go bonkers. I would have to be on serious drugs. I’d be super-duper bored. I like high intensity.”
            p ― Elon Musk
          .col-md-8.col-sm-12.button-row
            nuxt-link.main-button(to="/gallery") Gallery
            nuxt-link.main-button(to="/map") Map

      .col-md-6
        img(src="~@/assets/space.svg", width="100%")
  .row.scroll
    h3(v-html="addEmoji('scroll 👇 down')")
  .container-fluid.w100
    .min-h.row-container.container
      .box
        h1.coxh1 why i chosed this title?
        .row
          .col-md-8.thetextbox
            p.thetext These days our world is changing faster than ever, media and economy and in general, all parts of our society is related to the internet. Nowadays the leading subject of IT talks is 5G and how it will be helping our world and affects of that. But the forgotten thing that we can call a revolutionary invention is the Starlink. A network includes more than 12k satellites orbiting around our planet and brings us internet with no wires.
              br 
              | I, as a geek who loves tech and pays attention to it, choose this subject to introduce you Starlink.
        h4(v-html="addEmoji('thans our master ,🎓 Dr.Nariman Jahan')")
        h4(v-html="addEmoji('made with ❤️ love for web class')")
</template>

<script >
export default {
  methods: {
    addEmoji: function (text) {
      if (process.client) {
        let data = this.$twemoji.parse(text);
        return data;
      }
    },
  },
  mounted() {},
};
</script>

<style lang="scss">
.thetextbox {
  background: rgba(255, 255, 255, 0.6);
  font-size: 2em;
}
h4 > img.emoji {
  width: 1em;
}
h3 > img.emoji {
  width: 2em;
  -webkit-animation: slide-fwd-bottom 1s cubic-bezier(0.25, 0.46, 0.45, 0.94)
    infinite forwards;
  animation: slide-fwd-bottom 1s cubic-bezier(0.25, 0.46, 0.45, 0.94) infinite
    forwards;
  height: 2em;
  z-index: 2;
}
@-webkit-keyframes slide-fwd-bottom {
  0% {
    -webkit-transform: translateZ(0) translateY(0);
    transform: translateZ(0) translateY(0);
  }
  100% {
    -webkit-transform: translateZ(160px) translateY(50px);
    transform: translateZ(160px) translateY(50px);
    opacity: 0;
  }
}
@keyframes slide-fwd-bottom {
  0% {
    -webkit-transform: translateZ(0) translateY(0);
    transform: translateZ(0) translateY(0);
  }
  100% {
    -webkit-transform: translateZ(160px) translateY(50px);
    transform: translateZ(160px) translateY(50px);
    opacity: 0;
  }
}

.scroll {
  margin-top: -100px;
  height: 100px;
  text-align: center;
}
.coxh1 {
  color: white;
  mix-blend-mode: difference;
}
.w100 {
  /* Create the parallax scrolling effect */
  z-index: 9099;
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  background-image: url("https://www.spacex.com/static/images/crew-1/SN8.webp");
  height: 100vh;
}
.pt-100 {
  margin-top: 100px;
}
.navbar {
  width: 100vw;
  z-index: 999;
  background-color: white;
  padding-top: 5px;
  -webkit-box-shadow: 1px 9px 33px 2px rgba(0, 0, 0, 0.67);
  box-shadow: 1px 9px 33px 2px rgba(0, 0, 0, 0.67);
  top: 0px;
  position: absolute;
  padding-bottom: 10px;
}
.space {
  margin-bottom: 100px;
}
.page-enter-active,
.page-leave-active {
  transition-property: opacity;
  transition-timing-function: ease-in-out;
  transition-duration: 900ms;
}

.page-enter,
.page-leave-to {
  opacity: 0;
}
</style>  

<style lang="scss" scoped >
.button-row {
  flex-direction: row;
  justify-content: space-around;

  display: flex;
  margin-top: 20px;
}
.main-button {
  background-color: #55198b;
  border: solid 1px #55198b;
  color: white;
  font-weight: 700;
  width: max-content;
  padding: 13px 22px;
  margin-right: 50px;
  text-transform: uppercase;
  border-radius: 6px;
  text-align: center;
  text-decoration: none;
  display: block;
  margin-top: 20px;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.3s ease-in-out 0s;
}
.main-button:hover {
  background-color: #ffffff;
  color: #55198b;
  transition: all 0.3s ease 0s;
}
@import url("https://fonts.googleapis.com/css2?family=Montserrat+Alternates:wght@300&family=Montserrat+Subrayada&family=Montserrat:wght@200&display=swap");
h1 {
  font-family: "Montserrat Subrayada", sans-serif;
  font-size: 4em;
}
p {
  font-family: "Montserrat Alternates", sans-serif;
}
.p-5 {
  padding-top: 3vh;
  font-size: 1.6em;
}
.text-box {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.row-container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

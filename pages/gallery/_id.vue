<template lang="pug">
.app 
  .navbar
    .container 
      .row
        .col-3
          nuxt-link.main-button(to="/gallery") Gallery
  svg(
    width="380px",
    height="500px",
    viewBox="0 0 837 1045",
    version="1.1",
    xmlns="http://www.w3.org/2000/svg",
    xmlns:xlink="http://www.w3.org/1999/xlink",
    xmlns:sketch="http://www.bohemiancoding.com/sketch/ns"
  )
    g#Page-1(
      stroke="none",
      stroke-width="1",
      fill="none",
      fill-rule="evenodd",
      sketch:type="MSPage"
    )
      path#Polygon-1(
        d="M353,9 L626.664028,170 L626.664028,487 L353,642 L79.3359724,487 L79.3359724,170 L353,9 Z",
        stroke="#007FB2",
        stroke-width="6",
        sketch:type="MSShapeGroup"
      )
      path#Polygon-2(
        d="M78.5,529 L147,569.186414 L147,648.311216 L78.5,687 L10,648.311216 L10,569.186414 L78.5,529 Z",
        stroke="#EF4A5B",
        stroke-width="6",
        sketch:type="MSShapeGroup"
      )
      path#Polygon-3(
        d="M773,186 L827,217.538705 L827,279.636651 L773,310 L719,279.636651 L719,217.538705 L773,186 Z",
        stroke="#795D9C",
        stroke-width="6",
        sketch:type="MSShapeGroup"
      )
      path#Polygon-4(
        d="M639,529 L773,607.846761 L773,763.091627 L639,839 L505,763.091627 L505,607.846761 L639,529 Z",
        stroke="#F2773F",
        stroke-width="6",
        sketch:type="MSShapeGroup"
      )
      path#Polygon-5(
        d="M281,801 L383,861.025276 L383,979.21169 L281,1037 L179,979.21169 L179,861.025276 L281,801 Z",
        stroke="#36B455",
        stroke-width="6",
        sketch:type="MSShapeGroup"
      )

  .container.pt-100 
    vue-image-slider(:images="images", :intervalVal="5000")

    p(
      v-html="addEmoji(`${data.success != 'true' ? '✅' : '❌'} Suucess  ${data.success != 'true' ? 'yes ' : 'no'}`)"
    )
    p(v-html="addEmoji(`⏲ local time  ${data.date_local} `)")
    p {{ 'details : ' + data.details }}
</template>
<style >
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
img.emoji {
  height: 1em;
  width: 1em;
}
</style>
<style scoped>
img.emoji {
  height: 1rem;
  width: 1rem;
}
p {
  font-size: 1.5em;
}
li {
  padding: 3px;
}

svg {
  position: absolute;
  top: 20%;
  left: 30%;
  margin-top: -250px;
  margin-left: -400px;
}
.message-box {
  height: 200px;
  width: 380px;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -100px;
  margin-left: 50px;
  color: #fff;
  font-family: Roboto;
  font-weight: 300;
}
.message-box h1 {
  font-size: 60px;
  line-height: 46px;
  margin-bottom: 40px;
}
.buttons-con .action-link-wrap {
  margin-top: 40px;
}
.buttons-con .action-link-wrap a {
  background: #68c950;
  padding: 8px 25px;
  border-radius: 4px;
  color: #fff;
  font-weight: bold;
  font-size: 14px;
  transition: all 0.3s linear;
  cursor: pointer;
  text-decoration: none;
  margin-right: 10px;
}
.buttons-con .action-link-wrap a:hover {
  background: #5a5c6c;
  color: #fff;
}

#Polygon-1,
#Polygon-2,
#Polygon-3,
#Polygon-4,
#Polygon-4,
#Polygon-5 {
  animation: float 1s infinite ease-in-out alternate;
}
#Polygon-2 {
  animation-delay: 0.2s;
}
#Polygon-3 {
  animation-delay: 0.4s;
}
#Polygon-4 {
  animation-delay: 0.6s;
}
#Polygon-5 {
  animation-delay: 0.8s;
}

@keyframes float {
  100% {
    transform: translateY(20px);
  }
}
@media (max-width: 450px) {
  svg {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -250px;
    margin-left: -190px;
  }
  .message-box {
    top: 50%;
    left: 50%;
    margin-top: -100px;
    margin-left: -190px;
    text-align: center;
  }
}
</style>

<script>
import VueImageSlider from "~/components/slider.vue";
import axios from "axios";
export default {
  components: {
    VueImageSlider,
  },
  data() {
    return { data: {}, images: [] };
  },
  methods: {
    addEmoji: function (text) {
      if (process.client) {
        let data = this.$twemoji.parse(text);
        return data;
      }
    },
  },
  mounted() {
    let id = this.$route.params.id;
    axios.get("https://api.spacexdata.com/v4/launches").then((res) => {
      let data = res.data;
      this.data = data.find((launch) => launch.id == id);
      this.images = this.data.links.flickr.original;
    });
  },
};
</script>
<template lang="pug">
.app
  .navbar
    .container 
      .row
        .col-3
          nuxt-link.main-button(to="/") home
  h1.text-center(v-show="loadingStatus", v-html="loadingTextGenerator()") 
  .container.pt-100
    .row
      .card.col-md-4.col-sm-12(v-for="item in images", :key="item.id")
        vs-card.cardx(actionable="")
          div(slot="header")
          div(slot="media")
            img(:src="item.links.flickr.original[0]")
          .cut-text
            span {{ item.details }}
          div(slot="footer")
            vs-row(vs-justify="flex-end")
              nuxt-link(:to="`/gallery/` + item.id")
                vs-button(color="primary", type="gradient") View
    .row.show-morebtn 
      vs-button(
        v-show="!loadingStatus",
        @click="loadNewPage()",
        color="success",
        type="gradient"
      ) load More
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      loadingStatus: true,
      loadCount: 13,
      images: [],
      timer: 0,
    };
  },
  mounted() {
    this.updateData();
    setInterval(() => this.timer++, 1000);
  },
  methods: {
    loadingTextGenerator: function () {
      if (process.client) {
        let data = this.$twemoji.parse(
          "🤘I'll loading new data , ⌛It may take a while depending on your internet speed. Please be patient."
        );
        return (
          data +
          "<br> you spended : " +
          this.timer +
          " secounds waiting , pleas buy faster internet!"
        );
      }
    },
    loadNewPage: function () {
      this.loadCount += 12;
      this.loadingStatus = !this.loadingStatus;
      this.updateData();
    },
    updateData: function () {
      axios
        .get("https://api.spacexdata.com/v4/launches")
        .then((res) => {
          let images = res.data.filter(
            (itm) => itm.links.flickr.original.length != 0
          );
          this.images = images
            .slice(images.length - this.loadCount, images.length - 1)
            .reverse();
          this.loadingStatus = !this.loadingStatus;
        })
        .catch((err) => alert(err));
    },
  },
};
</script>

<style lang="scss" scoped>
.p20 {
  margin-left: 20vw;
}
.show-morebtn {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}
.cut-text {
  text-overflow: ellipsis;
  overflow: hidden;
  height: 1.2em;
  white-space: nowrap;
}
img {
  height: 150px;
  object-fit: cover;
}
.card {
  padding: 15px;
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
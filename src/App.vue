<template>
  <div id="app">
     <div class="container">
       <div class="row">
         <div class="col-3 mb-3" v-for="(item, index) in images" :key="index">
           <img class="img-fluid" :src="item.url" :alt="item.name" @click="openGallery(index)">
         </div>
       </div>
     </div>
      <GalleryModal v-if="showGallery.show" :config="showGallery"/>
  </div>
</template>

<script>
const GalleryModal = () => import('./components/GalleryModal.vue');

export default {
  name: 'App',
  data() {
    return {
      images: [
        {
          url: 'https://cdn.pixabay.com/photo/2020/03/01/12/36/fire-4892711_960_720.jpg',
          name: 'Photo 1',
        },
        {
          url: 'https://cdn.pixabay.com/photo/2019/03/15/09/49/girl-4056684_960_720.jpg',
          name: 'Photo 2',
        },
        {
          url: 'https://cdn.pixabay.com/photo/2020/11/20/01/10/glacier-5760277_960_720.jpg',
          name: 'Photo 3',
        },
        {
          url: 'https://cdn.pixabay.com/photo/2019/10/06/18/27/meadow-hogweed-4530921_960_720.jpg',
          name: 'Photo 4',
        },
        {
          url: 'https://cdn.pixabay.com/photo/2018/11/11/19/46/christmas-bauble-3809544_960_720.jpg',
          name: 'Photo 5',
        },
        {
          url: 'https://cdn.pixabay.com/photo/2020/10/03/14/54/rock-formations-5623735_960_720.jpg',
          name: 'Photo 6',
        },
        {
          url: 'https://cdn.pixabay.com/photo/2016/11/14/16/20/snowflake-1823942_960_720.jpg',
          name: 'Photo 7',
        },
        {
          url: 'https://cdn.pixabay.com/photo/2020/12/20/14/52/forest-5847268_960_720.jpg',
          name: 'Photo 8',
        }
      ],
      showGallery: {
        show: false,
        selector: Math.random().toString(36).substr(2, 9),
        data: null,
      },
    };
  },
  methods: {
    openGallery(index) {
      this.showGallery.show = true;
      this.showGallery.data = {
        medias: this.images,
        index,
      };
    },
  },
  components: {
    GalleryModal,
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

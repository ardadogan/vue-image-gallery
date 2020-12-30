<template>
  <div>
    <div
      class="modal fade"
      :id="config.selector"
      role="dialog"
    >
      <div class="slider">
        <div class="header">
          <div class="row w-100">
            <div class="col-10 col-md-6 pl-3 pl-lg-5 mt-3 d-flex justify-content-start align-items-center">
              <span class="pl-3 pr-5 c-white s-26">{{images[currentIndex].name}}</span>
            </div>
            <div class="col-2 col-md-6 d-flex justify-content-end align-items-center mt-3">
              <button type="button" class="close" data-dismiss="modal" title="Close" aria-label="Close" @click="close()">
                <span aria-hidden="true"><i class="fa fa-times-circle c-white"/></span>
              </button>
            </div>
          </div>
        </div>
        <div class="footer">
          <div class="col-md-12 d-flex justify-content-center">
            <span class="c-white s-26">{{currentIndex+1}} / {{images.length}}</span>
          </div>
        </div>
        <div class="col-md-10 d-flex justify-content-center align-items-center">
          <div class="arrows">
            <span class="click" @click="prev"><i class="fa fa-chevron-left fa-4x"></i></span>
            <span class="click" @click="next"><i class="fa fa-chevron-right fa-4x" ></i></span>
          </div>
          <div v-for="i in [currentIndex]" :key="i">
            <img v-if="currentImg.url" class="img-fluid pl-5 pr-5" :src="currentImg.url" alt=""/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GalleryModal',
  props: ['config'],
  data() {
    return {
      images: [],
      back: false,
      currentIndex: 0,
    };
  },
  methods: {
    close() {
      $(`#${this.config.selector}`).modal().hide();
      $('.modal-backdrop').remove();
      this.config.show = false;
    },
    next() {
      if (this.currentIndex !== this.images.length - 1) {
        this.currentIndex += 1;
        this.back = false;
      }
    },
    prev() {
      if (this.currentIndex > 0) {
        this.currentIndex -= 1;
        this.back = true;
      }
    },
    runModal(id) {
      $(id).modal({
        backdrop: 'static',
        keyboard: false,
      });
    },
    handleKeyDown(e) {
      if (e.keyCode === 39) {
        this.next();
      } else if (e.keyCode === 37) {
        this.prev();
      }
    }
  },
  mounted() {
    this.runModal(`#${this.config.selector}`);
    document.addEventListener("keyup", this.handleKeyDown);
  },
  computed: {
    currentImg() {
      return this.images[Math.abs(this.currentIndex) % this.images.length];
    },
  },
  watch: {
    config: {
      handler(n) {
        this.images = n.data.medias;
        this.currentIndex = n.data.index;
      },
      immediate: true,
      deep: true,
    },
  },
}
</script>

<style scoped>
.modal {
  background: #000000bf;
}
.c-white {
  color: #fff;
}
.s-26 {
  font-size: 26px;
}
.slider {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.arrows {
  display: flex;
  position: absolute;
  justify-content: space-between;
  width: 100%;
  align-items: center;
  color: #fff;
}
.header {
  position: absolute;
  width: 100%;
  display: flex;
  top: 10px;
  justify-content: space-between;
}
.footer {
  position: absolute;
  width: 100%;
  display: flex;
  bottom: 50px;
  justify-content: center;
}
.close {
  opacity: 1;
}
.img-fluid {
  max-height: 800px;
}
.click:hover {
  cursor: pointer;
}
</style>
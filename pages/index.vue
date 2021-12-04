<template>
  <div
    id="app"
  >
    <Flipbook
      class="flipbook"
      :pages="pictures"
      :singlePage="true"
      ref="flipbook"
    >
      <div class="action-bar">
        <span class="page-info">
          <b>
            Memories <br />
            #DevFestLAGOS 2021
          </b>
        </span>
      </div>
    </Flipbook>
  </div>
</template>

<script>
const PICTURE_URL = require("@/store/data");

export default {
  name: "App",
  data () {
    return {
      xDown: null,
      yDown: null,
      pictures: PICTURE_URL,
    }
  },

  methods: {
    GetTouches (event) {
      return event.touches || event.originalEvent.touches;
    }, //end of GetTouches

    HandleTouchStart (event) {
      const firstTouch = getTouches(event)[0];
      this.xDown = firstTouch.clientX;
      this.yDown = firstTouch.clientY;
    }, // end of HandleTouchStart

    HandleTouchMove (event) {
      event.preventDefault();
      if (!this.xDown || !this.yDown) return false;

      const flipbook = this.$refs.flipbook;

      const xUp = event.touches[0].clientX;
      const yUp = event.touches[0].clientY;
    
      const xDiff = this.xDown - xUp;
      const yDiff = this.yDown - yUp;
      
      if ( Math.abs( xDiff ) > Math.abs( yDiff ) ) {/*most significant*/
        if ( xDiff > 0 ) {
          /* left swipe */
          flipbook.flipLeft();
        } else {
          /* right swipe */
          flipbook.flipRight();
        }
      } else {
        if ( yDiff > 0 ) {
          /* up swipe */ 
          flipbook.zoomIn();
        } else {
          /* down swipe */
          flipbook.zoomOut();
        }
      }
      /* reset values */
      this.xDown = null;
      yDiff = null;     
    }, // end of HandleTouchMove

    GoToFullScreen () {
      const elem = document.documentElement;
      try {
        if (elem.requestFullscreen) {
          elem.requestFullscreen();
        } else if (elem.webkitRequestFullscreen) { /* Safari */
          elem.webkitRequestFullscreen();
        } else if (elem.msRequestFullscreen) { /* IE11 */
          elem.msRequestFullscreen();
        }
      } catch (error) {
        // console.log(error.message);
      }
      
    }, //end of GoToFullScreen
  },

  mounted () {
    window.addEventListener('keydown', event => {
      event.preventDefault();
        this.GoToFullScreen();
      const flipbook = this.$refs.flipbook;
      if ((event.key === "Left" || event.key === "ArrowLeft")) {
        // console.log("left pressed");
        flipbook.flipLeft();
      } else if ((event.key === "Right" || event.key === "ArrowRight")) {
        // console.log("right pressed");
        flipbook.flipRight();
      } else if ((event.key === "Up" || event.key === "ArrowUp")) {
        // console.log("right pressed");
        flipbook.zoomIn();
      } else if ((event.key === "Down" || event.key === "ArrowDown")) {
        // console.log("right pressed");
        flipbook.zoomOut();
      }
    }, true);

    document.addEventListener('touchstart', this.HandleTouchStart, false);
    document.addEventListener('touchmove', this.HandleTouchMove, false);

    alert(`
    Next Picture: Arrow key right or swipe right\n
    Previous Picture: Arrow key left or swipe left\n
    Zoom in: Arrow key up or double tap\n
    Zoom out: Arrow key down or double tap\n
    `);
  },
}
</script>

<style>

  html, body {
    margin: 0;
    padding: 0;
    height: 100%;
    overflow: hidden;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #333;
    color: #ccc;
    overflow: hidden;
  }

  .action-bar {
    width: 100%;
    height: 30px;
    padding: 10px 0;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 25px;
  }

  .action-bar .page-info {
    text-align: center;
    margin: 20px;
  }

  .flipbook {
    width: 90vw;
    height: calc(100vh - 50px - 40px);
  }

  .flipbook .viewport {
    width: 90vw;
    height: calc(100vh - 50px - 40px);
  }

  .flipbook .bounding-box {
    box-shadow: 0 0 20px #000;
  }


</style>
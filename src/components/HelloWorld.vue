<template>
  <div>
    <div class="hello" v-if="!isUploaded">
      <h1>Upload images</h1>
      <input type="file" id="imageLoader"  @change="updateCanvasImage">  
    </div>
    <div v-if="isUploaded">
      <canvas id="imageCanvas" ref="imageCanvas" class="preview-element"></canvas>
      <div class="filter-title">Brightness</div>
      <div class="input-container">
        <input type="range" @input="changeBrightness" min="0" max="255" step="1" v-model="value" >
      </div> 
    </div>
  </div>
</template>


<script>
import { upload } from "../file-upload.service";

export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      isUploaded: false,
      image: null,
      value: 0
    };
  },
  methods: {
    updateCanvasImage(e) {
      var self = this;

      var reader,
        files = e.target.files;

      var reader = new FileReader();

      reader.onload = e => {
        var img = new Image();
        img.onload = function() {
          self.image = img;
          self.drawCanvasImage(img);
        };
        img.src = event.target.result;
      };

      reader.readAsDataURL(files[0]);
      this.isUploaded = true;
    },
    drawCanvasImage(img) {
      var canvas = this.$refs.imageCanvas;
      canvas.width = img.width;
      canvas.height = img.height;

      var ctx = canvas.getContext("2d");
      ctx.drawImage(img, 0, 0);
    },
    changeBrightness(e) {
      var canvas = this.$refs.imageCanvas;
      canvas.width = this.image.width;
      canvas.height = this.image.height;

      var ctx = canvas.getContext("2d");

      ctx.drawImage(this.image, 0, 0);

      var imageData = ctx.getImageData(0, 0, this.image.width, this.image.height);
      var dataArray = imageData.data; 

      var brightnessMul = parseInt(this.value); // brightness multiplier

      for(var i = 0; i < dataArray.length; i += 4) {
        var red = dataArray[i]; 
        var green = dataArray[i + 1]; 
        var blue = dataArray[i + 2]; 

        var brightenedRed = brightnessMul + red;
        var brightenedGreen = brightnessMul + green;
        var brightenedBlue = brightnessMul + blue;

        dataArray[i] = Math.max(0, Math.min(255, brightenedRed));
        dataArray[i + 1] = Math.max(0, Math.min(255, brightenedGreen));
        dataArray[i + 2] = Math.max(0, Math.min(255, brightenedBlue));
      }

      ctx.putImageData(imageData, 0, 0);
      
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.filter-title {
  margin: 10px 0;
  font-size: 18px;
}

.input-container {
  background-color: white;
  width: 50%;
  height: 40px;
  margin: auto;
  display: flex;
  justify-content: center;
  align-items: center;
}

.hello {
  outline: 2px dashed grey; /* the dash box */
  outline-offset: -10px;
  background: lightcyan;
  color: dimgray;
  padding: 10px 10px;
  min-height: 200px; /* minimum height */
  position: relative;
  cursor: pointer;
}


.preview-element {
  width: 50%;
}


/*** Sytle the track ***/
input[type="range"] { 
    margin: auto;
    -webkit-appearance: none;
    position: relative;
    overflow: hidden;
    width: 90%;
    height: auto;
    cursor: pointer;
    border-radius: 0; /* iOS */
}

::-webkit-slider-runnable-track {
    background: #ddd;
    height: 5px;
}

/*
 * 1. Set to 0 width and remove border for a slider without a thumb
 */
::-webkit-slider-thumb {
    -webkit-appearance: none;
    width: 36px; /* 1 */
    height: 40px;
    background: #fff;
    border-radius: 50%;
    margin-top: -14px;
    box-shadow: -100vw 0 0 100vw dodgerblue, 0px 0px 1px #0d0d0d;
    border: 2px solid #999; /* 1 */
}

::-moz-range-track {
    height: 2px;
    background: #ddd;
}

::-moz-range-thumb {
    background: #fff;
    height: 36px;
    width: 36px;
    border: 3px solid #999;
    border-radius: 50%;
    box-shadow: -100vw 0 0 100vw dodgerblue;
    box-sizing: border-box;
}

::-ms-fill-lower { 
    background: dodgerblue;
}

::-ms-thumb { 
    background: #fff;
    border: 2px solid #999;
    height: 36px;
    width: 36px;
    box-sizing: border-box;
}

::-ms-ticks-after { 
    display: none; 
}

::-ms-ticks-before { 
    display: none; 
}

::-ms-track { 
    background: #ddd;
    color: transparent;
    height: 2px;
    border: none;
}

::-ms-tooltip { 
    display: none;
}


/*****/


</style>

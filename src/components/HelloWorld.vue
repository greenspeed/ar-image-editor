<template>
  <div>
    <div class="hello" v-if="!isUploaded">
      <h1>Upload images</h1>
      <input type="file" id="imageLoader"  @change="updateCanvasImage">  
    </div>
    <div v-if="isUploaded">
      <canvas id="imageCanvas" ref="imageCanvas"></canvas>
      <div>Brightness</div>
      <input type="range" @change="changeBrightness" min="0" max="255" step="1" v-model="value" class="brightness">
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

        dataArray[i] = brightenedRed;
        dataArray[i + 1] = brightenedGreen;
        dataArray[i + 2] = brightenedBlue;
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
.brightness {
  width: 50%;
}
</style>

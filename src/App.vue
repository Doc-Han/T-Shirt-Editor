<template>
  <div id="app">
    <div class="asideLeft">
    <asideLeft :config="config.left" ></asideLeft>
    </div>
    <div class="editor">
      <editor />
    </div>
    <div class="asideRight">
      <asideRight :config="config.right"></asideRight>
    </div>
  </div>
</template>

<script>
import asideLeft from './components/asideLeft'
import editor from './components/editor'
import asideRight from './components/asideRight'
import {rightToCanvas} from './main'

export default {
  name: 'app',
  components: {
    asideLeft,
    editor,
    asideRight,
  },
  data () {
    return {
      config: {
        left: {
          title: '',
          colors: ['#ffffff','#f44336','#009688','#ff9800','#795548','#607d8b'],
          selectedColor: '#ffffff',
        },
        right: {
          categories: ['Movies','Funny','Others'],
          selectedCategory: '',
          keywords: [],
          base: 35,
          profit: [5,10,15],
          selectedProfit: 5,
        }
      }
    }
  },
  created: function(){
    var _self = this; // to get the $el object :)
    rightToCanvas.$on('upload-click', function(d){
      _self.upload();
    });
  },
  methods: {
    upload: function(){
      console.log(this.config);
    }
  },
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}

$aside-width: 300px;
$editor-width: calc(80vw - 600px); // The value subtracted in here is ($aside-width * 2)
$window-heigth: 90vh;

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: $window-heigth;
  margin-top: 5vh;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

@mixin borderStyle(){
  border: 1px solid #e8e8e8;
  border-radius: 5px;
  background-color: #fbfbfb;
}

.asideLeft {
  flex-basis: $aside-width;
  @include borderStyle;
}

.editor {
  flex-basis: $editor-width;
}

.asideRight {
  flex-basis: $aside-width;
  @include borderStyle;
}

.content {
  width: $aside-width;
}

.input {

  margin-top: 10px;

  .label {
      margin-left: 10px;
      text-align: left;
  }
  .input-control {
    width: $aside-width - 40px;
    height: 30px;
    padding: 0 10px;
    outline: none;
    font-size: 20px;
    border-radius: 5px;
    border: 1px solid #e8e8e8;
  }

  .colors,.artworks,.inputTag {
    width: $aside-width - 40px;
    border: 1px solid #e8e8e8;
    margin: auto;
    padding: 10px 10px 0 10px;
  }
}



h1, h2 {
  font-weight: normal;
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
</style>

<template>
  <v-container>
          <v-row>
              <v-col cols="12">
              </v-col>
              <v-col cols="12">
              <h1 class="title font-weight-bold text-center">
                  TRANSLITERATION
              </h1>
              </v-col>
              <v-col cols="12">
              </v-col>
          </v-row> 
<!-- choose language from to TRANSLITERATION -->
          <v-row class="mb-12">
              <!-- <v-spacer></v-spacer> -->
           
              <v-col cols="5" class="text-center">
              <v-select
              v-model="e2"
              :items="['English']"
              menu-props="auto"
              hide-details
              label="Select"
              solo
              single-line
              >
              </v-select>
              </v-col>

              <v-col cols="2" class="text-center">
              <span class="font-weight-bold">TO</span>
              </v-col>

              <v-col cols="5" class="text-center">
              <v-select
              v-model="e1"
              :items="languages[0].name"
              menu-props="auto"
              hide-details
              label="Select"
              single-line
              solo
              v-on:change="changeLanguage()"
              >
              </v-select>
              </v-col>
              <!-- <v-spacer></v-spacer>  -->
          </v-row>    
  

      <!-- textarea where user right text for TRANSLITERATION -->

    <v-row class="">
    <v-textarea id="editor_area"
      clearable
      v-model='text'
      clear-icon="cancel"
      label="Text"
      v-on:keyup="myFunction()"
      solo
      outlined
      autofocus
    >
    </v-textarea>
    </v-row>

        <!-- <v-row class="mb-12"> -->

     <!-- suggestion dropdown       -->
     <div v-bind:style="styleObject">
         <v-select
                  v-model="category"
                  color="deep-purple accent-5"
                  :items="dropdown"
                  v-on:change="changeFunction(),openDropdown(0);"
                   outlined
                   
                >
         </v-select>
         
     </div>
      <!-- </v-row> -->

  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",

  data: () => ({
    cordx:5,
    cordy:6,
    styleObject: {
        position: 'absolute',
        display: "none",
        left:5 + 'px',
        top: 6 + 'px'
    },
    e1: "Hindi",
    e2: "English",
    languages: [
              {
               name:["Hindi", "Tamil", "Telugu", "Bengali", "Gujarati", "Marathi", "Kannada", "Malayalam", "Punjabi", "Nepali"]
              },
              {
               nickName:["hindi", "tamil", "telugu", "bengali", "gujarati", "marathi", "kannada", "malayalam", "punjabi", "nepali"]
              }
              ],
    text: "",
    temp: "",
    category: "",
    dropdown: []
  }),
  mounted(){

     window.addEventListener('mousemove',this.mouseIsMoving);
     // eslint-disable-next-line no-undef
     if(localStorage.getItem("language")==true)
     this.e1 = localStorage.getItem("language");
}, 
  methods: {
changeLanguage(){
localStorage.setItem("language", this.e1);

},
    async myFunction() {
      
      this.styleObject.display = "block"
      var txtarea = document.getElementById("editor_area");
     var rect = txtarea.getBoundingClientRect();

  this.styleObject.left = txtarea.selectionStart + rect.left + 'px'; 
    this.styleObject.top = rect.top + 'px'; 
      var i=0,lang;
      while(this.e1 != this.languages[0].name[i])
      {
        i++;
      }
      lang = this.languages[1].nickName[i];
      this.temp = this.text.split(" ");
      let url =
        "http://146.148.85.67/processWordJSON?inString=" +
        this.temp[this.temp.length - 1] +
        "&lang="+lang;
      await axios.post(url).then(data => {
        this.dropdown = [...data.data.twords[0].options];
      });
    },
    changeFunction() {
      if (this.text.search(" ") == -1) 
        this.text = this.category + " ";
      else
        this.text = this.text.slice(0, this.text.lastIndexOf(" ")) + " " + this.category + " ";

        this.styleObject.display = "none";
        document.getElementById("editor_area").focus();
        this.category = "";
    },

    openDropdown() {
    var dropdown = document.getElementById('myDropDown');
    var event;
    event = document.createEvent('MouseEvents');
    event.initMouseEvent('mousedown', true, true, window);
    dropdown.dispatchEvent(event);
}
  }
};
</script>

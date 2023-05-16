<template>
    <div class="about">
        <h1>{{infoSurah.id + ". " + infoSurah.name_simple + " (" + infoSurah.name_arabic + ")"}}</h1>
    </div>
    <li v-for="(item,index) in listContohSurah">
        {{item.text_uthmani}}
        <p v-html="arti[index].text"></p>
    </li>
  </template>
  
  <script>
  import axios from "axios";
  import { ref } from 'vue';
  export default {
      data() {
          return {
              infoSurah: ref([]),
              listSurah: ref([]),
              listContohSurah: ref([]),
              arti: ref([])
          }
      },
  
      mounted() {
          this.getInfoSurah()
          this.getListChapter()
          this.getListContohSurah()
          this.getArti()
      },
  
      methods: {
          getInfoSurah() {
              axios.get('https://api.quran.com/api/v4/chapters/1?language=id')
                  .then((respons) => {
                      console.log(respons)
                      this.infoSurah = respons.data.chapter
                  }).catch((err) => {
                  console.log('error' + err)
              })
          },
          getListChapter() {
              axios.get('https://api.quran.com/api/v4/chapters?language=en')
                  .then((respons) => {
                      console.log(respons)
                      this.listSurah = respons.data.chapters
                  }).catch((err) => {
                  console.log('error ' + err)
              })
          },
          getListContohSurah() {
              axios.get('https://api.quran.com/api/v4/quran/verses/uthmani?chapter_number=1')
                  .then((respons) => {
                      console.log(respons)
                      this.listContohSurah = respons.data.verses
                  }).catch((err) => {
                      console.log('error' + err)
                  })
          },
          getArti() {
              axios.get('https://api.quran.com/api/v4/quran/translations/33?chapter_number=1')
                  .then((respons) => {
                      console.log(respons)
                      this.arti = respons.data.translations
                  }).catch((err) => {
                      console.log('error' + err)
              })
        }
    }
}


         
    
  </script>
  
  <style>
  
  </style>
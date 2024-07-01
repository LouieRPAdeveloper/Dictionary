<script setup lang="ts">
import HelloWorld from "./components/HelloWorld.vue";
import Headerproy from "./components/Headerproy.vue";
import Linterior from "./components/Linterior.vue";
import { ref } from "vue";

const inputValue = ref("");
const palabra = ref("");
const pronuncio = ref("");
const firstword = ref("");
const meaningword = ref("");
const urldefinea = ref("");
const synomymsword = ref("");
const jsonmeaning = ref("");
let sound = ref("");
let audioaudio = ref("");

async function fetchData(url: string): Promise<any> {
  const response = await fetch(url);

  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }

  const data = await response.json();
  return data;
}

fetchData("https://api.dictionaryapi.dev/api/v2/entries/en/police")
  .then((data) => {
    console.log(data);
    console.log(data[0].word);
    console.log(data[0]["phonetic"]);
    console.log(data[0].sourceUrls[0]); //sourceUrls
    console.log(data[0].meanings[0]["partOfSpeech"]);
    console.log(data[0]["phonetics"].length);
    palabra.value = data[0].word;
    pronuncio.value = data[0]["phonetic"];
    firstword.value = data[0].meanings[0]["partOfSpeech"];
    urldefinea.value = data[0].sourceUrls[0];
    meaningword.value = data[0].meanings[0]["definitions"][1]["definition"];
    jsonmeaning.value = data[0].meanings[0]["definitions"];
    synomymsword.value = data[0].meanings[0]["definitions"][1]["definition"];
    for (let i = 0; i < data[0]["phonetics"].length; i++) {
      if (data[0]["phonetics"][i]["audio"].length != 0) {
        audioaudio = data[0]["phonetics"][i]["audio"];
        console.log("hay 1 audio");
        break;
      }
    }
  })
  .catch((error) => console.error(error));

function playSound(sound) {
  if (sound) {
    var audio = new Audio(sound);
    audio.play();
  }
}

function fuenteverdana() {
  console.log("fuente verdana");
}

function cambiapalabra() {
  console.log("dfsdfsd");
  fetchData(
    "https://api.dictionaryapi.dev/api/v2/entries/en/" + this.inputValue,
  )
    .then((data) => {
      console.log(data);
      console.log(data[0].word);
      console.log(data[0]["phonetic"]);
      console.log(data[0].sourceUrls[0]); //sourceUrls
      console.log(data[0].meanings[0]["partOfSpeech"]);
      console.log(data[0]["phonetics"].length);
      palabra.value = data[0].word;
      pronuncio.value = data[0]["phonetic"];
      firstword.value = data[0].meanings[0]["partOfSpeech"];
      urldefinea.value = data[0].sourceUrls[0];
      meaningword.value = data[0].meanings[0]["definitions"][1]["definition"];
      jsonmeaning.value = data[0].meanings[0]["definitions"];
      synomymsword.value = data[0].meanings[0]["definitions"][1]["definition"];
      for (let i = 0; i < data[0]["phonetics"].length; i++) {
        if (data[0]["phonetics"][i]["audio"].length != 0) {
          audioaudio = data[0]["phonetics"][i]["audio"];
          console.log("hay 1 audio");
          break;
        }
      }
    })
    .catch((error) => console.error(error));
}
</script>

<template>
  <header>
    <div class="container d-flex flex-wrap border-bottom">
      <ul class="nav me-auto">
        <li class="nav-item">
          <a
            href="\project\sandbox\index.html"
            class="nav-link link-body-emphasis px-2 active"
            aria-current="page"
            ><i class="bi bi-journal-album"></i> Dictionary</a
          >
        </li>
        <li class="nav-item">
          <a href="#" class="nav-link link-body-emphasis px-2"></a>
        </li>
        <li class="nav-item">
          <a href="#" class="nav-link link-body-emphasis px-2"></a>
        </li>
        <li class="nav-item">
          <a href="#" class="nav-link link-body-emphasis px-2"></a>
        </li>
        <li class="nav-item">
          <a href="#" class="nav-link link-body-emphasis px-2"></a>
        </li>
      </ul>
      <ul class="nav">
        <li class="nav-item">
          <div class="dropdown">
            <button
              class="btn btn-secondary dropdown-toggle"
              type="button"
              data-bs-toggle="dropdown"
              aria-expanded="false"
            >
              Select type
            </button>
            <ul class="dropdown-menu">
              <li>
                <button @click.prevent="fuenteverdana()" class="dropdown-item">
                  Verdana
                </button>
              </li>
              <li>
                <button @click.prevent="fuenteserif()" class="dropdown-item">
                  Serif
                </button>
              </li>
              <li>
                <button @click.prevent="fuenteroman()" class="dropdown-item">
                  Times New Roman
                </button>
              </li>
            </ul>
          </div>
        </li>
        <li class="nav-item">
          <a href="#" class="nav-link link-body-emphasis px-2"
            ><i class="bi bi-moon-fill"></i> Dark Mode</a
          >
        </li>
      </ul>
    </div>
  </header>

  <div class="input-group mb-3 mt-5">
    <input
      v-model="inputValue"
      type="text"
      class="form-control"
      placeholder="Write the word"
      aria-label="word"
      aria-describedby="basic-addon1"
    />
    <button
      @click.prevent="cambiapalabra()"
      type="button"
      class="btn btn-secondary"
    >
      <i class="bi bi-search"></i>
    </button>
  </div>

  <div class="d-flex justify-content-between mb-3 mt-5">
    <div class="d-flex flex-column">
      <h2>{{ palabra }}</h2>
      <p class="d-flex justify-content-start">{{ pronuncio }}</p>
    </div>

    <button
      type="button"
      @click.prevent="playSound(audioaudio)"
      class="btn btn-outline-secondary"
    >
      <i class="bi bi-play"></i>
    </button>
  </div>

  <h6 id="word" class="d-flex justify-content-start mt-5">
    {{ firstword }}
  </h6>
  <!--ul>
    <li type="disc" class="d-flex justify-content-start mt-5">
      {{ meaningword }}
    </li>
  </ul-->
  <Linterior
    class="d-flex justify-content-start mt-0 mb-2 py-0"
    v-for="project in jsonmeaning"
    :key="project.definition"
    :pao="project.definition"
  />

  <!--p id="rea">listas</p-->

  <p class="d-flex justify-content-start mt-5">
    Synonyms: <span id="synonymwords" class="px-1"> {{ synomymsword }}</span>
  </p>

  <h6 class="d-flex justify-content-start mt-5">
    Source URL: {{ urldefinea }}
  </h6>

  <!--h6 class="d-flex justify-content-start mt-5">
    {{ audioaudio }}
  </h6-->

  <!--Linterior
    class="d-flex justify-content-start mt-5"
    v-for="project in jsonmeaning"
    :key="project.definition"
    :pao="project.definition"
  /-->

  <br />
  <!--Linterior pao="dfds" /-->
  <!--HelloWorld msg="Vite + Vue" /-->
</template>

<style scoped>
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css");

* {
  /*font-family: verdana;*/
  /*font-family: Times New Roman;*/
  /*font-family: Arial;*/
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
#rea {
  color: red;
}
</style>

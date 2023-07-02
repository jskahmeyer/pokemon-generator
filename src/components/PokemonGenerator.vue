<style scoped lang="scss">
body {
  background: #fff;
}

main {
  font-family: "GothamPro", sans-serif;
  padding: 2rem 0;
}

label {
  margin-top: 10px;
}

.form-container {
  background-color: #fafafa;
  border-radius: 10px;
  box-shadow: 0px 3px 15px rgba(0,0,0,0.2);
  padding: 40px;
}

.btn-demo {
  margin-left: 10px;
  color: #0d6efd;
  border: none;
  background-color: transparent;
}

.image-goes-here {
  display: none;
}

.image-capture {
  background: #002b49;
  box-shadow: 0px 3px 15px rgba(0,0,0,0.2);
  border-radius: 22px;
  height: 590px;
  margin: 0;
  overflow: hidden;
  padding: 0;
  position: relative;
  width: 420px;

  &.real-image {
    left: -800%;
    position: fixed;
    top: 0;
  }
}

.background-image {
  left: 0;
  position: absolute;
  top: 0;
  width: 100%;
  z-index: 2;
}

.fake-download-link {
  display: none;
}

.pokemon-card-image {
  position: relative;

  .image-capture {
    background: #fff;
  }

  .pokemon-name {
    width: 160px;
    font-size: 20px;
    font-weight: 700;
    color: #000;
    position: absolute;
    font-family: sans-serif;
    text-align: left;
    top: 22px;
    left: 110px;
    z-index: 999;
  }

  .pokemon-hp {
    position: absolute;
    top: 24px;
    left: 312px;
    text-align: left;
    z-index: 9;
    font-weight: bold;
    font-size: 18px;
  }

  .hp-label {
    font-size: 10px;
  }

  .pokemon-image-container {
    position: absolute;
    top: 50px;
    left: 30px;
    height: 250px;
    width: 365px;
    z-index: 999;
    background-size: cover;
    z-index: 1;
  }

  .pokemon-moves-container {
    position: absolute;
    top: 330px;
    left: 30px;
    height: 140px;
    width: 360px;
    z-index: 9;
    text-align: left;
  }

  .pokemon-move-name {
    font-weight: bold;
  }

  .pokemon-move-description {
    font-size: 12px;
  }

  .pokemon-type-icon {
    width: 14px;
    height: 14px;
  }

  .pokemon-type-icon-lg {
    width: 20px;
    height: 20px;
  }

  .weakness-icon {
    position: absolute;
    z-index: 9;
    top: 514px;
    left: 35px;
  }

  .resistance-icon {
    position: absolute;
    z-index: 9;
    top: 514px;
    left: 111px;
  }

  .retreat-icon {
    position: absolute;
    z-index: 9;
    top: 554px;
    left: 35px;
  }

  .shape {
    width: 50px;
    height: 60px;
    shape-outside: polygon(46px 0, 47px 0, 6px 50px, 5px 50px);
    float: left;
  }

  .shape2 {
    width: 50px;
    height: 60px;
    shape-outside: polygon(49px 0, 50px 0, 9px 50px, 8px 50px);
    float: right;
  }

  .parallelogram {
    text-align: left;
    position: absolute;
    top: 495px;
    right: 30px;
    width: 210px;
    height: 60px;
    padding: 4px;
    z-index: 9;
  }

  .parallelogram p {
    padding-top: 5px;
    width: 200px;
    height: 46px;
    font-size: 8px;
    font-style: italic;
    line-height: 9px;
  }
}
</style>

<template>
  <div class="my-5 container">
    <h1 class="text-center mb-5">Pokemon Generator</h1>
    <div class="row justify-content-between">
      <div class="col-xl-7 mb-5">
        <div class="form-container">
          <div class="form-group">
            <h3>Build Your Pokemon!</h3>
            <div class="form-group">
              <label for="selectType"> Select Type</label>
              <select id="selectType" class="form-select" v-model="type">
            <option selected disabled value="">Select Type</option>
            <option v-for="pt in pokemonTypes" :key="pt" :value="pt.toLowerCase()">
              {{ pt }}
            </option>
              </select>
            </div>
            <div class="row">
              <div class="col-md-6 form-group">
                <label for="name">Name</label>
                <input id="name" class="form-control" type="text" v-model="name" maxlength="14"/>
              </div>
              <div class="col-md-6 form-group">
                <label for="hp">HP</label>
                <input id="hp" class="form-control" type="number" v-model="hp" maxlength="3"/>
              </div>
            </div>
            <div class="form-group">
              <label for="imgInput">Image URL</label><button @click="image = 'rainbow-pikachu.jpeg'" class="btn-demo"><small>Use demo image</small></button>
              <input id="imgInput" class="form-control" type="text" v-model="image" />
            </div>
            <hr class="mt-4">
            <div class="row mt-3">
              <div class="col-md-6">
                <h5 class="mb-0">Move #1</h5>
                <div class="form-group">
                  <label for="move1name">Name</label>
                  <input id="move1name" class="form-control" type="text" v-model="move1name" />
                </div>
                <div class="row">
                  <div class="col-6">
                    <label for="move1type1">Type</label>
                    <select id="move1type1" class="form-select" v-model="move1type1">
            <option selected disabled value="">Select Type</option>
            <option v-for="pt in pokemonTypes" :key="pt" :value="pt.toLowerCase()">
              {{ pt }}
            </option>
                    </select>
                  </div>
                  <div class="col-6">
                    <label for="move1type2">Type 2</label>
                    <select id="move1type2" class="form-select" v-model="move1type2">
            <option selected disabled value="">Optional</option>
            <option v-for="pt in pokemonTypes" :key="pt" :value="pt.toLowerCase()">
              {{ pt }}
            </option>
                    </select>
                  </div>
                </div>
                <div class="form-group">
                  <label for="move1description">Description</label>
                  <textarea
                    id="move1description"
                    class="form-control"
                    type="text"
                    v-model="move1description"
                    maxlength="140"
                  ></textarea>
                </div>
              </div>
              <div class="col-md-6">
                <h5 class="mb-0">Move #2</h5>
                <div class="form-group">
                  <label for="move2name">Name</label>
                  <input id="move2name" class="form-control" type="text" v-model="move2name" />
                </div>
                <div class="row">
                  <div class="col-6">
                    <label for="move2type1">Type</label>
                    <select id="move2type1" class="form-select">
            <option selected disabled value="">Select Type</option>
            <option v-for="pt in pokemonTypes" :key="pt" :value="pt.toLowerCase()">
              {{ pt }}
            </option>
                    </select>
                  </div>
                  <div class="col-6">
                    <label for="move2type2">Type 2</label>
                    <select id="move2type2" class="form-select" v-model="move2type2">
            <option selected disabled value="">Optional</option>
            <option v-for="pt in pokemonTypes" :key="pt" :value="pt.toLowerCase()">
              {{ pt }}
            </option>
                    </select>
                  </div>
                </div>
                <div class="form-group">
                  <label for="move2description">Description</label>
                  <textarea
                    id="move2description"
                    class="form-control"
                    type="text"
                    v-model="move2description"
                    maxlength="140"
                  ></textarea>
                </div>
              </div>
            </div>
            <hr class="mt-4">
            <div class="row">
              <div class="col-md-4 form-group">
                <label for="weaknessType">Weakness</label>
                <select id="weaknessType" class="form-select" v-model="weaknessType">
            <option selected disabled value="">Select Type</option>
            <option v-for="pt in pokemonTypes" :key="pt" :value="pt.toLowerCase()">
              {{ pt }}
            </option>
                </select>
              </div>
              <div class="col-md-4 form-group">
                <label for="resistanceType">Resistance</label>
                <select id="resistanceType" class="form-select" v-model="resistanceType">
            <option selected disabled value="">Select Type</option>
            <option v-for="pt in pokemonTypes" :key="pt" :value="pt.toLowerCase()">
              {{ pt }}
            </option>
                </select>
              </div>
              <div class="col-md-4 form-group">
                <label for="retreatType">Retreat</label>
                <select id="retreatType" class="form-select" v-model="retreatType">
            <option selected disabled value="">Select Type</option>
            <option v-for="pt in pokemonTypes" :key="pt" :value="pt.toLowerCase()">
              {{ pt }}
            </option>
                </select>
              </div>
            </div>
            <div class="col-md-6 form-group">
              <label for="excerpt">Tell Us About Your Pokemon</label>
              <textarea id="excerpt" class="form-control" v-model="excerpt" maxlength="208"></textarea>
            </div>
          </div>
        </div>
      </div>
      <div class="col-xl-5 text-center">
        <div class="pokemon-card-image">
          <div class="image-capture-container pb-5">
            <div class="image-capture mx-auto">
              <div class="pokemon-name">{{ name }}</div>
              <div class="pokemon-hp">
                <span class="hp-label">HP</span>{{ hp }}
              </div>
              <div
                class="pokemon-image-container"
                :style="{ backgroundImage: `url('${image}')` }"
              ></div>
              <div class="pokemon-moves-container">
                <div class="row mb-3">
                  <div class="col-md-3">
                    <img
                      v-if="move1type1" class="pokemon-type-icon-lg"
                      :src="getPokemonIcon(move1type1)"
                    />
                    <img
                      v-if="move1type2"
                      class="pokemon-type-icon-lg"
                      :src="getPokemonIcon(move1type2)"
                    />
                  </div>
                  <div class="pokemon-move-name col-md-9">{{ move1name }}</div>
                  <div class="col-12">
                    <p class="pokemon-move-description">
                      {{ move1description }}
                    </p>
                  </div>
                </div>
                <div class="row">
                  <div class="col-md-3">
                    <img
                      v-if="move2type1" 
                      class="pokemon-type-icon-lg"
                      :src="getPokemonIcon(move2type1)"
                    />
                    <img
                      v-if="move2type2"
                      class="pokemon-type-icon-lg"
                      :src="getPokemonIcon(move2type2)"
                    />
                  </div>
                  <div class="pokemon-move-name col-md-9">{{ move2name }}</div>
                  <div class="col-12">
                    <p class="pokemon-move-description">
                      {{ move2description }}
                    </p>
                  </div>
                </div>
              </div>
              <img
              v-if="weaknessType" 
                class="pokemon-type-icon weakness-icon"
                :src="getPokemonIcon(weaknessType)"
              />
              <img
              v-if="resistanceType" 
                class="pokemon-type-icon resistance-icon"
                :src="getPokemonIcon(resistanceType)"
              />
              <img
              v-if="retreatType" 
                class="pokemon-type-icon retreat-icon"
                :src="getPokemonIcon(retreatType)"
              />
              <div class="parallelogram">
                <div class="shape"></div>
                <div class="shape2"></div>
                <p class="pokemon-excerpt">{{ excerpt }}</p>
              </div>
              <img class="background-image" :src="getBackgroundImage(type)" />
            </div>

            <div id="capture" class="image-capture real-image">
                            <div class="pokemon-name">{{ name }}</div>
              <div class="pokemon-hp">
                <span class="hp-label">HP</span>{{ hp }}
              </div>
              <div
                class="pokemon-image-container"
                :style="{ backgroundImage: `url('${image}')` }"
              ></div>
              <div class="pokemon-moves-container">
                <div class="row mb-3">
                  <div class="col-md-3">
                    <img
                      v-if="move1type1" class="pokemon-type-icon-lg"
                      :src="getPokemonIcon(move1type1)"
                    />
                    <img
                      v-if="move1type2"
                      class="pokemon-type-icon-lg"
                      :src="getPokemonIcon(move1type2)"
                    />
                  </div>
                  <div class="pokemon-move-name col-md-9">{{ move1name }}</div>
                  <div class="col-12">
                    <p class="pokemon-move-description">
                      {{ move1description }}
                    </p>
                  </div>
                </div>
                <div class="row">
                  <div class="col-md-3">
                    <img
                      v-if="move2type1" 
                      class="pokemon-type-icon-lg"
                      :src="getPokemonIcon(move2type1)"
                    />
                    <img
                      v-if="move2type2"
                      class="pokemon-type-icon-lg"
                      :src="getPokemonIcon(move2type2)"
                    />
                  </div>
                  <div class="pokemon-move-name col-md-9">{{ move2name }}</div>
                  <div class="col-12">
                    <p class="pokemon-move-description">
                      {{ move2description }}
                    </p>
                  </div>
                </div>
              </div>
              <img
              v-if="weaknessType" 
                class="pokemon-type-icon weakness-icon"
                :src="getPokemonIcon(weaknessType)"
              />
              <img
              v-if="resistanceType" 
                class="pokemon-type-icon resistance-icon"
                :src="getPokemonIcon(resistanceType)"
              />
              <img
              v-if="retreatType" 
                class="pokemon-type-icon retreat-icon"
                :src="getPokemonIcon(retreatType)"
              />
              <div class="parallelogram">
                <div class="shape"></div>
                <div class="shape2"></div>
                <p class="pokemon-excerpt">{{ excerpt }}</p>
              </div>
              <img class="background-image" :src="getBackgroundImage(type)" />
        
            </div>
          </div>
          <button
            v-on:click="saveImage()"
            type="button"
            class="btn btn-lg btn-primary"
          >
            Download Pokemon Card
          </button>
          <div class="image-goes-here"></div>
          <a class="fake-download-link" :href="imageSrc" download="image.png"
            >Save Image - Fake</a
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import html2canvas from "html2canvas"

export default {
  data() {
    return {
      name: "",
      hp: "",
      move1name: "",
      move1type1: "",
      move1type2: "",
      move1description: "",
      move2name: "",
      move2type1: "",
      move2type2: "",
      move2description: "",
      weaknessType: "",
      resistanceType: "",
      retreatType: "",
      excerpt: "",
      image: "",
      imageSrc: false,
      type: "colorless",
      pokemonTypes: [
        "Colorless",
        "Dark",
        "Fighting",
        "Fire",
        "Grass",
        "Lightning",
        "Psychic",
        "Steel",
        "Water"
      ]
    };
  },
  methods: {
    getBackgroundImage: function (type) {
      let url = require("@/assets/images/cards/" + type + "-type-blank.png");
      return url;
    },
    getPokemonIcon: function (type) {
      let url = require("@/assets/images/icons/" + type + "-icon.png");
      return url;
    },
    saveImage: function () {
      html2canvas(document.querySelector("#capture"), {
        proxy: "proxy.js",
        useCORS: true,
        logging: true,
      })
        .then((canvas) => {
          if (document.querySelector(".image-goes-here canvas")) {
            document.querySelector(".image-goes-here canvas").remove();
          }

          document.querySelector(".image-goes-here").appendChild(canvas);

          let dataURL = canvas.toDataURL("image/png");
          this.imageSrc = dataURL;
        })
        .finally(() => {
          document.querySelector(".fake-download-link").click();
        });
    },
  },
};
</script>
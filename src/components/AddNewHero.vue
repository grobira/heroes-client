<template>
    <div class="newHero">
        <h1>New Hero</h1>
        <template>
          <b-container fluid>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>First Name :</label></b-col>
              <b-col sm="9"><b-form-input type="text" v-model="firstname"></b-form-input></b-col>
            </b-row>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>Last Name :</label></b-col>
              <b-col sm="9"><b-form-input type="text" v-model="lastname"></b-form-input></b-col>
            </b-row>
            <b-row class="hero-form-row">
                <b-col sm="3"><label>Class :</label></b-col>
                <b-col sm="9">
                    <b-form-group>
                        <b-form-select :options="classNames" required v-model="selectClass"></b-form-select>
                    </b-form-group>
                </b-col>
            </b-row>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>Breed :</label></b-col>
              <b-col sm="9">
                    <b-form-group>
                        <b-form-select :options="breeds" required v-model="selectBreed"></b-form-select>
                    </b-form-group>
                </b-col>
            </b-row>
            <b-row class="hero-form-row">Initial Status</b-row>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>Str :</label></b-col>
              <b-col sm="9"><input class="slider" type="range" :max="pointsAvaliable.str" v-model="heroStr">{{heroStr}}</b-col>
            </b-row>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>Int :</label></b-col>
              <b-col sm="9"><input class="slider" type="range" :max="pointsAvaliable.int" v-model="heroInt">{{heroInt}}</b-col>
            </b-row>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>Lck :</label></b-col>
              <b-col sm="9"><input class="slider" type="range" :max="pointsAvaliable.lck" v-model="heroLck">{{heroLck}}</b-col>
            </b-row>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>Dex :</label></b-col>
              <b-col sm="9"><input type="range" class="slider" :max="pointsAvaliable.dex" v-model="heroDex">{{heroDex}}</b-col>
            </b-row>
            <b-row class="hero-form-row">
                <b-progress class="hero-form-bar" :value="pointsAvaliable.total" :min=0 :max="max" show-progress></b-progress>
            </b-row>
            <b-row class="hero-form-row">
                <b-button type="submit" variant="primary" class="hero-form-button" @click="addHero">Submit</b-button>
            </b-row>
          </b-container>
        </template>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'AddNewHero',
    data () {
        return {
            classNames: [],
            breeds: [],
            max: 100,
            heroLck: 0,
            heroInt: 0,
            heroStr: 0,
            heroDex: 0,
            selectBreed: '',
            selectClass: '',
            firstname: '',
            lastname: '',
        }
    },
    computed :{
        pointsAvaliable() {
            return { total: this.max - this.heroStr - this.heroInt - this.heroLck - this.heroDex,
                    str: this.max - this.heroInt - this.heroLck - this.heroDex,
                    int: this.max - this.heroStr - this.heroLck - this.heroDex,
                    lck: this.max - this.heroInt - this.heroStr - this.heroDex,
                    dex: this.max - this.heroInt - this.heroLck - this.heroStr
                    };
        },
    },
    mounted () {
        axios
        .get('http://localhost:3001/classes').then(response => {
            response.data.forEach(element => {
                this.classNames.push(element.name);
            });
        });
        axios
        .get('http://localhost:3001/breeds').then(response => {
            response.data.forEach(element => {
                this.breeds.push(element.name);
            });
        });
    },
    methods: {
        addHero(){
            var body = {
                "firstname" : this.firstname,
                "lastname" : this.lastname,
                "class": this.selectClass,
                "breed": this.selectBreed,
                "status" : {
                    "str": this.heroStr,
                    "int": this.heroInt,
                    "lck": this.heroLck,
                    "dex": this.heroDex
                }
            }

            axios.post('http://localhost:3001/heroes/', body).then( 
                this.$emit("heroAdded", "Hero Added")
            );
        }
    }
}
</script>

<style>
.newHero {
    width: 100%;
    height: 617px;
}

h1 {
    font-size: 58px;
}

.hero-form-row {
    height: 50px;
}

.hero-form-button {
    margin-left: 15%; 
}

.hero-form-bar {
    background-color: dimgray;
    width: 100%;
}

.slider {
    -webkit-appearance: none;
    height: 10px;
    width: 100%;
    border-radius: 5px;   
    background: #d3d3d3;
    outline: none;
    opacity: 0.7;
    -webkit-transition: .2s;
    transition: opacity .2s;
}

.slider::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 15px;
    height: 15px;
    border-radius: 50%; 
    background: #06940d;
    cursor: pointer;
}

.slider::-moz-range-thumb {
    width: 15px;
    height: 15px;
    border-radius: 50%;
    background: #06940d;
    cursor: pointer;
}
</style>

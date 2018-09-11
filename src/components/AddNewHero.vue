<template>
    <div class="newHero">
        <h1>New Hero</h1>
        <template>
          <b-container fluid>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>Name :</label></b-col>
              <b-col sm="9"><b-form-input type="text"></b-form-input></b-col>
            </b-row>
            <b-row class="hero-form-row">
                <b-col sm="3"><label>Class :</label></b-col>
                <b-col sm="9">
                    <b-form-group>
                        <b-form-select :options="classNames" required></b-form-select>
                    </b-form-group>
                </b-col>
            </b-row>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>Breed :</label></b-col>
              <b-col sm="9">
                    <b-form-group>
                        <b-form-select :options="breeds" required></b-form-select>
                    </b-form-group>
                </b-col>
            </b-row>
            <b-row class="hero-form-row">Initial Status</b-row>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>Str :</label></b-col>
              <b-col sm="9"><input class="slider" type="range" v-model="heroStr">{{heroStr}}</b-col>
            </b-row>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>Int :</label></b-col>
              <b-col sm="9"><input class="slider" type="range" v-model="heroInt">{{heroInt}}</b-col>
            </b-row>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>Lck :</label></b-col>
              <b-col sm="9"><input class="slider" type="range" v-model="heroLck">{{heroLck}}</b-col>
            </b-row>
            <b-row class="hero-form-row">
              <b-col sm="3"><label>Dex :</label></b-col>
              <b-col sm="9"><input type="range" min="1" max="100" value="50" class="slider" v-model="heroDex">{{heroDex}}</b-col>
            </b-row>
            <b-row class="hero-form-row">
                <b-progress class="hero-form-bar" :value="pointsAvaliable" :min=0 :max="max" show-progress></b-progress>
            </b-row>
            <b-row class="hero-form-row">
                <b-button type="submit" variant="primary" class="hero-form-button">Submit</b-button>
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
            breeds: [ 'human', 'elf'],
            max: 100,
            heroLck: 0,
            heroInt: 0,
            heroStr: 0,
            heroDex: 0,
        }
    },
    computed :{
        pointsAvaliable() {
            return 100 - this.heroStr - this.heroInt - this.heroLck - this.heroDex;
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

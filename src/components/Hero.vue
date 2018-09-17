<template>
<div class="HeroMenu">
  <h1>Heroes Battles MS</h1>
  <div>
    <b-tabs class="tabs-menu">
      <b-tab title="Heroes" active>
        <b-container class="bv-example-row">
          <b-row>
              <b-col><AddNewHero @heroAdded="refreshHeroList" ref="heroList"/></b-col>
              <b-col><HeroesList/></b-col>
          </b-row>
        </b-container>        
      </b-tab>
      <b-tab title="Battle" >
        <br>Battle Module
      </b-tab>
      <b-tab title="To do" disabled>
        <br>Disabled tab!
      </b-tab>
    </b-tabs>
  </div>
</div>
</template>

<script>
import AddNewHero from './AddNewHero'
import HeroesList from './HeroesList'

export default {
  name: 'Hero',
  components: { 
    AddNewHero,
    HeroesList
  },
  props: {
    msg: String
  },
  methods: {
    refreshHeroList() {
      console.log('catch event');
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.HeroMenu {
  width: 70%;
  height: 80%;
  left: 11%;
  position: fixed;
}

h1 {
  margin: 40px 0 0 0;
  left: 11%;
  position: fixed;
}
a {
    background-color: #42b983;
}
.tabs-menu {
  margin: 100px 0 0 0;
  left: 11% + 10px;
  width: 70%;
  height: 80%;
  position: fixed;
}
</style>

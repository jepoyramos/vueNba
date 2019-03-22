<template>
 <div class="c-team">
    <flickity v-if="Object.keys(playerStanding).length > 0" ref="flickity" :options="flickityOptions">
      <div v-for='(player, index) in playerStanding.slice(0, 3)' :key="index" class="carousel-cell">
        <span>{{player.firstName + " " + player.lastName}}<br/>
        {{player.rating}}</span>
      </div>
    </flickity>
     <ul class="o-team">
       <li v-if="visibility"><h2>Team A</h2></li>
        <li :class="player.class" v-for='(player, index) in team.slice(0, 5)' :key="index" >
          {{player.firstName + " " + player.lastName}}<br/>
          <span>Ratings: {{player.rating}}</span>
        </li>
        <li v-if="visibility">Team Rating: {{totalRating(team.slice(0, 5))}}</li>
     </ul>
     <ul class="o-team">
       <li v-if="visibility"><h2>Team B</h2></li>
       <li :class="player.class" v-for='(player, index) in team.slice(5, 10)' :key="index" >
         {{player.firstName + " " + player.lastName}}<br/>
         <span>Ratings: {{player.rating}}</span>
        </li>
        <li v-if="visibility">Team Rating: {{totalRating(team.slice(5, 10))}}</li>
     </ul>
     <button @click="createTeam()">Create Team</button>
 </div>
</template>

<script>
import Flickity from 'vue-flickity'

export default {
  name: 'Team',
  components: {
    Flickity
  },
  data () {
    return{
      team:[],
      playerStanding:[],
      visibility: false,
      flickityOptions: {
        initialIndex: 1,
        prevNextButtons: true,
        pageDots: false,
        wrapAround: true,
        autoPlay: true
      }
    }
  },
  props: {
    playersList: {}
  },
  methods: {
    createTeam(){
      this.team = [];
      let counter;
      let random;
      let currentPlayerID;
      for(counter=0; counter < 10; counter++){
        random = Math.floor(Math.random() * 541) + 1;
        this.newPLayer = this.playersList[random];
        currentPlayerID = this.newPLayer.playerId;
        if(this.isExisting(currentPlayerID) === false){
          this.team.push(this.newPLayer);
          this.createRating(counter);
        }else{
          // console.log("player " + currentPlayerID + " Existing");
        }
      }
      this.visibility = true;
      this.getTopRates();
    },
    isExisting(player){
      let existing = this.team.some(el => el.playerId === player);
      return existing;
    },
    createRating(playerSelect){
      let rating = Math.floor(Math.random() * (90 - 70)) + 70;
      this.team[playerSelect].rating = rating;
      this.assignClass(playerSelect, rating);
    },
     totalRating(team){
      let total = 0;
      let counter;
      for(counter=0; counter<team.length; counter++){
          total += team[counter].rating;
      }
      return Math.round(total/team.length);
    },
    assignClass(playerSelect, rating){
      if (rating == 90 || rating >= 85){
        this.rateClass = "color--green";
      }else if (rating <= 84 && rating >= 80){
        this.rateClass = "color--orange";
      }else if(rating <= 79) {
        this.rateClass = "color--red";
      }
      this.team[playerSelect].class = this.rateClass;
    },
    getTopRates(){
      this.playerStanding.push(...this.team);      
      this.playerStanding.sort(function(playerY,playerX){
        if(playerY.rating < playerX.rating){ return 1; } 
        else if(playerY.rating == playerX.rating) { return 0; } 
        else { return -1; }
      });
    },
    next() {
      this.$refs.flickity.next();
    },
    previous() {
      this.$refs.flickity.previous();
    } 
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .o-team{
    display: inline-block;
    vertical-align: top;
  }
  ul{
      padding: 0;
  }
  li{
    display: block;
    color: White;
    border: dashed 1px teal;
    padding: 10px;
    list-style-type: none;
    text-align: left;
     &:nth-child(1){
      text-align: center;
    }
    &:nth-child(-n+4){
      border-bottom: 0;
    }
  }
  .color--green{
    span{
      color: #058304;
    }
  }
  .color--orange{
    span{
      color: #fea401;
    }
  }
  .color--red{
    span{
      color: #fe0401;
    }
  }
  button{
    display: block;
    margin: 0 auto;
    padding: 10px;
    border: 0;
    border-radius: 25px;
    cursor: pointer;
    background: teal;
    text-align: center;
    color: white;
  }
  .carousel {
    background: #EEE;
  }
  .carousel-cell {
    width: 66%;
    height: 200px;
    margin-right: 10px;
    background: #8C8;
    border-radius: 5px;
    counter-increment: carousel-cell;
    span{
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100%;
      color: white;
      font-size: 40px;
    }
  }
</style>

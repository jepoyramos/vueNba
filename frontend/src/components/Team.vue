<template>
 <div class="c-team">
     <ul class="o-team">
       <li v-show="visibility"><h2>Team A</h2></li>
        <li v-for='(player, index) in teamA' :key="index">
          {{player.firstName + " " + player.lastName}}<br/>
          Ratings: {{player.rating}}
        </li>
        <li v-show="visibility">Team Rating: {{totalRating(this.teamA)}}</li>
     </ul>
     <ul class="o-team">
       <li v-show="visibility"><h2>Team B</h2></li>
       <li v-for='(player, index) in teamB' :key="index">
         {{player.firstName + " " + player.lastName}}<br/>
         Ratings: {{player.rating}}
        </li>
        <li v-show="visibility">Team Rating: {{totalRating(this.teamB)}}</li>
     </ul>
     <button @click="createTeam()">Create Team</button>
 </div>
</template>

<script>
export default {
  name: 'Team',
  data () {
    return{
      teamA: [],
      teamB: [],
      teamRating: [],
      visibility: false
    }
  },
  props: {
    playersList: {}
  },
  methods: {
    createTeam(){
      this.teamA= [];
      this.teamB= [];
      let random;
      let counter;
      for(counter=0; counter < 10; counter++){
        random = Math.floor(Math.random() * 541) + 1;
        if(this.teamA.length != 5){                        
            this.teamA.push(this.playersList[random]);
            this.createRating(this.teamA, counter);
        }else{
            this.teamB.push(this.playersList[random]);
            this.createRating(this.teamB, counter);
        }
      }
      this.visibility = true;
    },
    createRating(team, playerSelect){
      let rating;
      let x = 5;
      rating = Math.floor(Math.random() * (90 - 70)) + 70;
      if(team === this.teamB){
        playerSelect = playerSelect - x;
        x--;
      }
      team[playerSelect].rating = rating;
    },
    totalRating(team){
      let total = 0;
      let counter;
      for(counter=0; counter<team.length; counter++){
          total += team[counter].rating;
      }
      return Math.round(total/team.length);
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
    color: teal;
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
</style>

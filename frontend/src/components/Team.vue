<template>
 <div class="c-team">
     <ul class="o-team">
       <li v-show="visibility"><h2>Team A</h2></li>
        <li :class="player.class" v-for='(player, index) in team' :key="index" v-if="index <= 4">
          {{player.firstName + " " + player.lastName}}<br/>
          <span>Ratings: {{player.rating}}</span>
        </li>
        <li v-show="visibility">Team Rating: {{totalRating("A")}}</li>
     </ul>
     <ul class="o-team">
       <li v-show="visibility"><h2>Team B</h2></li>
       <li :class="player.class" v-for='(player, index) in team' :key="index" v-if="index >= 5">
         {{player.firstName + " " + player.lastName}}<br/>
         <span>Ratings: {{player.rating}}</span>
        </li>
        <li v-show="visibility">Team Rating: {{totalRating("B")}}</li>
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
      team:[],
      teamRating: [],
      rateClass: "",
      visibility: false
    }
  },
  props: {
    playersList: {}
  },
  methods: {
    // createTeam(){
    //   this.teamA= [];
    //   this.teamB= [];
    //   let random;
    //   let counter;
    //   for(counter=0; counter < 10; counter++){
    //     random = Math.floor(Math.random() * 541) + 1;
    //     if(this.teamA.length != 5){
    //       // this.isExisting(this.teamA, counter);                   
    //       this.teamA.push(this.playersList[random]);
    //       this.createRating(this.teamA, counter);
    //     }else{
    //       // this.isExisting(this.teamB, counter);
    //       this.teamB.push(this.playersList[random]);
    //       this.createRating(this.teamB, counter);
    //     }
    //   }
    //   this.visibility = true;
    // },
    createTeam(){
      this.team = [];
      let counter;
      let random;
      for(counter=0; counter < 10; counter++){
        random = Math.floor(Math.random() * 541) + 1;
        this.team.push(this.playersList[random]);
        this.createRating(this.team, counter);
      }
      this.visibility = true;
      console.log(this.team);
    },
    // isExisting(team, playerSelect){
    //   let x = 5;
    //   if(team === this.teamB){
    //     playerSelect = playerSelect - x;
    //     x--;
    //   }
    //   console.log(team[playerSelect].playerId);
      
    //   team.map((k,v) => {
    //       return `ID ${team[k]}playerId;
    //   })
    // },
    createRating(team, playerSelect){
      let rating;
      // let x = 5;
      rating = Math.floor(Math.random() * (90 - 70)) + 70;
      
      // if(team === this.teamB){
      //   playerSelect = playerSelect - x;
      //   x--;
      // }
      team[playerSelect].rating = rating;
      this.assignClass(team, playerSelect, rating);
      
    },
    assignClass(team, playerSelect, rating){
      if (rating == 90){
        this.rateClass = "color--green";
      }else if (rating <= 89 && rating >= 80){
        this.rateClass = "color--orange";
      }else if(rating <= 79) {
        this.rateClass = "color--red";
      }
      team[playerSelect].class = this.rateClass;
    },
    totalRating(team){
      let total = 0;
      let counter;
      let sort;
      if(team == "A"){
        sort = 4;
      }else{
        sort = 9;
      }
      for(counter=0; counter<sort.length; counter++){
          total += team[counter].rating;
      }
      return Math.round(total/team.length);
    }
  },
  computed: {
    teamCreated(){
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
</style>

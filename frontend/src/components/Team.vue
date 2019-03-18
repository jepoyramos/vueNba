
<template>
 <div class="c-team">
     <ul class="o-team">
       <li v-show="visibility"><h2>Team A</h2></li>
        <li :class="player.class" v-for='(player, index) in team' :key="index" v-if="index <= 4"><!--  v-if="index <= 4" -->
          {{player.firstName + " " + player.lastName}}<br/>
          <span>Ratings: {{player.rating}}</span>
        </li>
        <!-- <li v-show="visibility">Team Rating: {{totalRating("A")}}</li> -->
     </ul>
     <ul class="o-team">
       <li v-show="visibility"><h2>Team B</h2></li>
       <li :class="player.class" v-for='(player, index) in team' :key="index" v-if="index >= 5"><!--  v-if="index >= 5" -->
         {{player.firstName + " " + player.lastName}}<br/>
         <span>Ratings: {{player.rating}}</span>
        </li>
        <!-- <li v-show="visibility">Team Rating: {{totalRating("B")}}</li> -->
     </ul>
     <button @click="createTeam()">Create Team</button>
 </div>
</template>

<script>
export default {
  name: 'Team',
  data () {
    return{
      team:[],
      visibility: false
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
      for(counter=0; counter < 10; counter++){
        random = Math.floor(Math.random() * 541) + 1;
        this.team.push(this.playersList[random]);
        // this.createRating(this.team, counter);
      }
      this.visibility = true;
      this.teamCreated;
    },
    segTeam(player, index){
      // let teamX;
      // let counter;
      // for(counter = 0; counter < 4; counter++){

      // }
      console.log(player);
      console.log(index);
      if(index <=4){
        this.teamX.push(player);
      }
      
    }
  },
  computed: {
    teamCreated(){
        console.log(this.team);
        this.team.map(this.segTeam);
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

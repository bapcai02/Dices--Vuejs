<template>
	<div id="app">

		 <div class="wrapper clearfix">
            <players
				v-bind:activePlayer = "activePlayer"
				v-bind:scoresPlayer = "scoresPlayer"
				v-bind:curentScore = "curentScore"
			/>
			<controls
				v-on:handelNewGame = "handelNewGame"
				v-on:handelRollDice = "handelRollDice"
				v-on:handelHold = "handelHold"
				v-bind:finalScore = "finalScore"
				v-on:handelfinalScore = "handelfinalScore"
			/>
            <dices	
				v-bind:Dices = "Dices"
			/>
			<popup-rule
				v-on:handelConfim = "handelConfim"
				v-bind:isOpenpopup = "isOpenpopup"
			/>
        </div>

	</div>
</template>

<script>
import Players 		from "./components/Players.vue";
import Controls 	from "./components/Controls.vue";
import Dices 		from "./components/Dices.vue";
import PopupRule    from "./components/PopupRule.vue";
export default {
	name: 'app',
	data () {
		return {
			isPlaying:false,
			isOpenpopup:false,
			activePlayer : 1,
			Dices : [5,1],
			scoresPlayer : [12,13],
			curentScore : 20,
			finalScore : 100,
		}
	},
	methods:{
		handelNewGame(){
			this.isOpenpopup = true;
		},
		handelHold(){
			if(this.isPlaying){
				let { scoresPlayer, activePlayer,curentScore} = this;
				let scoreOld = scoresPlayer[activePlayer];
				let cloneScorePlayer = [...scoresPlayer];
				cloneScorePlayer[activePlayer] = scoreOld + curentScore;
				this.scoresPlayer = cloneScorePlayer;
				this.nextPlayer();
			}
			else{
				alert('vui lòng nhấn new game');
			}
		},
		handelfinalScore(e){
			var number = parseInt(e.target.value);
			cosole.log(number);
		},
		nextPlayer(){
			this.activePlayer = this.activePlayer === 0 ? 1 : 0 ;
			this.curentScore = 0;
		},
		handelRollDice(){
			if(this.isPlaying){
				var dice1 = Math.floor(Math.random() * 6 ) + 1;
				var dice2 = Math.floor(Math.random() * 6 ) + 1;
				this.Dices = [dice1 , dice2];

				if(dice1 ===1 || dice2 === 1){
					setTimeout(function(){
						alert("rất tiếc bạn đã quay vào số 1, đổi người chơi")
					},10)
					this.nextPlayer();
				}
				else{
					this.curentScore = this.curentScore + dice1 + dice2;
				}
			}
			else{
				alert('vui lòng nhấn new game');
			}
		},
		handelConfim(){
			this.isPlaying = true;
			this.isOpenpopup = false;
			this.activePlayer = 0;
			this.scoresPlayer = [0,0];
			this.Dices = [1,1];
			this.curentScore = 0;
		},
		
	},
	components:{
		Players,
		Controls,
		Dices,
		PopupRule
	}
}
</script>

<style>
	* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('/public/assets/back.jpg');
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}

</style>

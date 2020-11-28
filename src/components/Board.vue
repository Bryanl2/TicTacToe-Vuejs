<template>
    <div class="container">
            <h1 class="title">Tic <span>Tae</span>  Toe</h1>

        <div class="status-action">
            
            <Status :winner="winner.player" :player="player" :isDrawGame="isDrawGame"/>
            
            <div class="reset" @click="resetGame">Reset</div>
        </div>
        <div class="game-grid">
            <Square v-for="(squareValue,position) in squares" :key="position" :value="squareValue" @click="onSquareClick(position)" />
               
        </div>
    </div>
    
</template>

<script>
import Status from './Status'
import Square from './Square'
import WhoWins from '../../solutionTicTacToe/winner'


export default {
    name:"Board",
    components:{
        Square,
        Status
    },
     data() {
    return {
      player: "x",
      squares: Array(9).fill(null)
    };
  },
  methods:{
      onSquareClick(position){

          if(this.squares[position]){
              return;
          }

          this.$set(this.squares,position,this.player);
          this.player=this.player==='x' ? "o": "x";
      },
      resetGame(){
          return this.squares=Array(9).fill(null);
      }
  },
  computed:{
      
      winner(){
          return WhoWins(this.squares);
      },
      isDrawGame(){
          return this.squares.filter(square=>!square).length===0;
      }
  }
  
}
</script>

<style >
*{
    box-sizing: border-box;
    margin:0;
    padding:0;
}

body{
    display:flex;
    font-family: sans-serif;
    justify-content: center;
   

}

.container{
    background: rgb(218, 45, 82);
    margin:50px;
    padding:50px;
    border-radius: 35px;
}

.title{
    text-align: center;
    font-size: 35px;
    margin-bottom: 10px;
    padding-bottom: 20px ;
    
}

.title span {
    color:#F2EBD3;
}


.status-action{
    display: flex;
    flex-wrap: wrap;
    font-size: 18px;
    justify-content: space-between;
    align-items: center;
    margin:15px 50px 15px 50px;
    height:30px;
}

.status span{
    color:#F2EBD3;
}

.reset, .game-status{
    cursor:pointer;
    font-size: 31px;
    color:rgb(49, 35, 35);
    font-weight: bold;
    
}

.reset:hover, .game-status:hover{
    color:#F2EBD3;
}

.game-grid{
    background:rgb(39, 29, 90);
    display:grid;
    grid-template-columns: repeat(3,1fr) ;
    grid-template-rows: repeat(3,1fr);
    grid-gap:15px;
    margin-top: 35px;
    
    border: solid rgb(13, 35, 77);
    border-width: 13px;
}

.game-cell{
    height: 200px;
    cursor:pointer;
    width: 200px;
    font-size: 150px;
    display: flex;
    justify-content: center;
    background:rgb(69, 69, 122);
    align-items: center;
    padding-bottom: 5px;
    color: rgb(207, 218, 207);
}

.game-cell-x{
    height: 200px;
    cursor:pointer;
    width: 200px;
    font-size: 150px;
    display: flex;
    justify-content: center;
    background:rgb(69, 69, 122);
    align-items: center;
    padding-bottom: 5px;
    color: rgb(174, 187, 174);
}
.game-cell-o{
    height: 200px;
    cursor:pointer;
    width: 200px;
    font-size: 150px;
    display: flex;
    justify-content: center;
    background:rgb(69, 69, 122);
    align-items: center;
    padding-bottom: 5px;
    color: rgb(16, 19, 16);
}

.game-cell:hover{
    background:rgb(61, 54, 102);
}


.x::after{
    content:'×';
    font-size: 200px;
}

.o::after{
    content:'o';
    font-size: 190px;
    margin: auto;
    color:#F2EBD3;
}


</style>
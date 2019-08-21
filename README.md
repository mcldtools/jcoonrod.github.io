
  <p><button onclick="startGame()">Shuffle</button></p>
  <div id=s0 class=s onclick="tempAlert('Freecell 0',1000)"></div>
  <div id=s1 class=s onclick="alert('Freecell 1')"></div>
  <div id=s2 class=s onclick="alert('Freecell 2')"></div>
  <div id=s3 class=s onclick="alert('Freecell 3')"></div>
  <div id=s4 class=s onclick="alert('Ace 0')"></div>
  <div id=s5 class=s onclick="alert('Ace 1')"></div>
  <div id=s6 class=s onclick="alert('Ace 2')"></div>
  <div id=s7 class=s onclick="alert('Ace 3')"></div>
  <div id=c0 class=c onclick="alert('Col 0')"></div>
  <div id=c1 class=c onclick="alert('Col 1')"></div>
  <div id=c2 class=c onclick="alert('Col 2')"></div>
  <div id=c3 class=c onclick="alert('Col 3')"></div>
  <div id=c4 class=c onclick="alert('Col 4')"></div>
  <div id=c5 class=c onclick="alert('Col 5')"></div>
  <div id=c6 class=c onclick="alert('Col 6')"></div>
  <div id=c7 class=c onclick="alert('Col 7')"></div>
<script>
// Set up a 1-d array of the unicode values for the cards 0-51
// Note - Unicode sets up 16 cards per suit, including two queens
  cards = []; // unicode for each card
  deck = []; // sort order for the cards
  aces = [[],[],[],[]]; // 2-d stacks in the aces positions
  freecells = [-1,-1,-1,-1]; // 4 free cells -1 indicates they are free
  stacks = [[],[],[],[],[],[],[],[]]; // 8 column stacks of cards

  for (n=0;n<52;n++) {
    deck[n]=n; // start out without a shuffle
    var suit=Math.floor(n/13);
    var val = n % 13; if (val>10) val++;  // jump over the extra queen
    cards[n]=127137+suit*16+val;
  }


// a function to shuffle the deck;
  function shuffle(){
    for(i=0; i<100; i++) { // do 100 random interchanges
      j=Math.floor(52*Math.random());
      k=Math.floor(52*Math.random());
      m=deck[j]; deck[j]=deck[k]; deck[k]=m;
    }
  }
// a function to deal the deck into the 8 stacks
  function deal(){
    for(j=0;j<8;j++) {
      stacks[j].length=0;
    }
    for(n=0;n<52;n++){
      j=n % 8;
      stacks[j].push(deck[n]);
    }
  }
// a function to show the stacks
  function showStacks(){
    stacks.forEach(showStack);
  }
function showStack(stack,j){
  // first strip off the existing children
  const column=document.getElementById("c"+j);
  while (column.firstChild) {
    column.removeChild(column.firstChild);
  }
  n=stack.length;
  for(i=0;i<n;i++) {
    var card=document.createElement("div");
    var cardNo=stack[i];
    var c='b'; if(cardNo>12 && cardNo<39) c='r'; // are the cards red or black?
    card.className=c;
    uni="&#"+cards[cardNo]+";";
    card.innerHTML=uni;
    card.style.zindex=i.toString();
    card.style.position='absolute';
    y=i*3;
    card.style.top=y.toString()+"vw";
    column.appendChild(card);
  }
}
  function startGame(){
    shuffle();
    deal();
    showStacks();
  }
  function tempAlert(msg,duration) { // adapted from Travis J on stackoverflow
     var el = document.createElement("div");
     el.className='a';
     el.innerHTML = msg;
     setTimeout(function(){
      el.parentNode.removeChild(el);
     },duration);
     document.body.appendChild(el);
  }

</script>

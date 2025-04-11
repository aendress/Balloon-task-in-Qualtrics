Qualtrics.SurveyEngine.addOnload(function()
{
	/*Place your JavaScript here to run when the page loads*/
	// standard version of the BART

$(document).ready(function() { 

  // Define file sources. We will create the corresponding objects below
  // we will select the correct image based on the risk level (i.e., the color of the balloon) below
  var imageSrc = "https://cityunilondon.eu.qualtrics.com/ControlPanel/File.php?F=F_40Tzn0HhGZ6aH2P";
  var explosionSoundSrc = "https://cityunilondon.eu.qualtrics.com/ControlPanel/File.php?F=F_avyGHMOPzwFlCj7";
  var tadaSoundSrc = "https://cityunilondon.eu.qualtrics.com/ControlPanel/File.php?F=F_8KNsaaULnXzdboK";
	
  // Choose risk level 
  // This will determine the color of the balloon, and the total number of trials
  // Currently set to unknown so it has no effect	 
  var risk_level = 'unknown'; // could be low|medium|high
	
  // initialize values
  var round = 0;
  var start_size = 150; // start value of widht & height of the image; must correspond to the value that is specified for the #ballon id in style.css
  var increase = 2; // number of pixels by which balloon is increased each pump
  var size; // start_size incremented by 'increase'
  var pumps; 
  var thanks;
  var maximal_pumps = 32;
  var pumpmeup; // number pumps in a given round; is updated each round
  var number_pumps = []; // arrays for saving number of pumps
  var total = 0; // money that has been earned in total
  var explosion; // will an explosion occur? 1 = yes, 0 = no
  var last_win = 0; // initialize variable that contains the win of the previous round
  var present_win = 0; //initialize variable of win in present around
  var rounds_played = 10;
  var exploded = []; // array for saving whether ballon has exploded
  //var explode_array =  [15, 9,  16, 26, 22,  8, 27,  17, 23,  29,];
  var BurstProb; //Random variable that determines whether balloon burst
  
  // adjust parameters according to risk level
  if (risk_level == 'low') {
 	// blue balloon
 	imageSrc = "https://cityunilondon.eu.qualtrics.com/ControlPanel/File.php?F=F_40Tzn0HhGZ6aH2P";
 	maximal_pumps = 128;
 	rounds_played = 30;
  } else if (risk_level == 'medium') {
 	// yellow balloon (use the b)
 	imageSrc = 'xxx';
 	maximal_pumps = 32;
 	rounds_played = 30;  
  } else if (risk_level == 'high') {
    // orange balloon (is actually red, as I don't have an orange one)
 	imageSrc = "https://cityunilondon.eu.qualtrics.com/ControlPanel/File.php?F=F_hY1EabrdLWtP8Ps";
 	maximal_pumps = 8;
 	rounds_played = 30;  
  } else {
  	console.log("Unknown risk level, continuing with defaults")	
  }
						
  // initialize language
  var label_press = 'Inflate balloon';
  var label_collect = 'Collect earnings';
  var label_balance = 'Total earnings:';
  var label_last = 'Earnings last round:';
  var label_currency = ' points';
  var label_times=' times';
  var label_header = 'Balloon Game Round ';
  var label_gonext1 = 'Start next round';
  var label_gonext2 = 'End game';
  var msg_explosion1 = '<p>The balloon exploded after pumping ';
  var msg_explosion2 = ' times.</p> <p>Once inflated, the balloon burst, and you did not earn any money this round.</p>';
  var label_present_time = 'Pumps made:';
  var label_present_value = 'Earnings this round:';		

  
  var msg_collect1 = '<p>The balloon did not burst!</p><p>In this round, you earned ';
  var msg_collect2 = ' points. </p> <p> The money you earned is safe in the bank.</p>';

  var msg_end1 = '<p>This completes this part of the study. You have earned ';
  var msg_end2 = ' points.</p> <p> Click <i>Next</i> to continue the study.</p>';
  
  // create sound and image objects
  // Dynamically insert audio elements
  var explosionSound = $('<audio>', {
	id: 'explosion_sound',
	src: explosionSoundSrc,
	preload: 'auto'
  });
  $('body').append(explosionSound);

  var tadaSound = $('<audio>', {
	id: 'tada_sound',
	src: tadaSoundSrc,
	preload: 'auto'
  });
  $('body').append(tadaSound);
  
  // Dynamically insert balloon image
  var balloonImg = $('<img>', {
	id: 'ballon',
	src: imageSrc,
	alt: 'Balloon',
	css: {
    	height: start_size + 'px',
	    width: start_size + 'px',
    	marginRight: 'auto',
	    marginLeft: 'auto',
    	marginBottom: '-380px',
    	display: 'none' // hidden until game starts
  	}
  });
  $('#ballonwrap').append(balloonImg);
  
  // initialize labels 
  $('#press').html(label_press); 
  $('#collect').html(label_collect);
  $('#total_term').html(label_balance);
  $('#total_value').html(total+label_currency);
  $('#last_term').html(label_last);
  $('#last_value').html(last_win+label_currency);
  $('#present_value_term').html(label_present_value);
  $('#present_times_term').html(label_present_time);
  $('#present_value').html(present_win+label_currency);
  $('#present_times').html(pumpmeup+label_times);
  $('#outcomes').html(number_pumps);
  
  // below: create functions that define game functionality
  
  // what happens when a new round starts
  var new_round = function() {
    //console.log(number_pumps);
    //console.log(exploded);
    $('#gonext').hide();
    $('#message').hide();  
    $('#collect').show();
    $('#press').show();
	$('#present_times').show();
	$('#present_value').show();
    round += 1;
    size = start_size;
    pumps = 0;
	present_win =0;
	show_present();
	show_present_earns();
    $('#ballon').width(size); 
    $('#ballon').height(size);
    $('#ballon').show();
    $('#round').html('<h2>'+label_header+round+'</h2>');
	$('#present_round').show();
	$('#outcomes').hide();
	$('#NextButton').hide();
  };
  
  // what happens when the game ends
  var end_game = function() {
    $('#total').remove();
    $('#collect').remove();
    $('#ballon').remove();
    $('#press').remove();
    $('#gonext').remove();
    $('#round').remove();
    $('#last_round').remove();
    $('#goOn').show();
    $('#message').html(msg_end1+total+msg_end2).show();
	$('#outcomes').show();
	$('#NextButton').show();
	Qualtrics.SurveyEngine.setEmbeddedData('number_pumps',number_pumps);
        Qualtrics.SurveyEngine.setEmbeddedData('exploded',exploded);
	Qualtrics.SurveyEngine.setEmbeddedData('total_win',total);

	
  };
  
  // message shown if balloon explodes
  var explosion_message = function() {
    $('#collect').hide();
    $('#press').hide();
    $('#message').html(msg_explosion1+pumpmeup+msg_explosion2).show();
  };
  
  // message shown if balloon does not explode
  var collected_message = function() {
    $('#collect').hide();
    $('#press').hide();    
    $('#message').html(msg_collect1+present_win+msg_collect2).show();
  };  

  // animate explosion using $ UI explosion
  var balloon_explode = function() {
    $('#ballon').hide( "explode", {pieces: 100}, 800 );
    document.getElementById('explosion_sound').play();
  };  
  
  // show button that starts next round
  var gonext_message = function() {
    $('#ballon').hide();
    if (round < rounds_played) {
      $('#gonext').html(label_gonext1).show();
    }
    else {
      $('#gonext').html(label_gonext2).show();
    }
  };

  // add money to bank
  var increase_value = function() {
    $('#total_value').html(total+label_currency);
  };
  
  var show_last = function() {
    $('#last_value').html(last_win+label_currency);
  };
  var show_present=function(){
	$('#present_times').html(pumps+label_times)
  }
  var show_present_earns=function(){
	$('#present_value').html(present_win+label_currency)
  }
   var show_array=function(){
	   $('#pump_array').html(number_pumps)
   }
  
  // button functionalities
  
  // pump button functionality -> 'pressure' in slider bar increases
  $('#press').click(function() {
     BurstProb = Math.random(); //generate random number between 0 and 1
    if (pumps >= 0 && pumps < maximal_pumps) { // interacts with the collect function, which sets pumps to -1, making the button temporarily unclickable
      explosion = 0; // is set to one if pumping goes beyond explosion point; see below
      pumps += 1;
	  present_win +=0.25;
	  //Burst probabilty is 1 / (maximal_pumps-pumps+1) as in Read et al. in 2002, so probability to burst increase with number of pumps, pumping becomes more risky
	  //Because BurstProb is random number between 0 and 1, the propbability that BurstProb > 1/(maximal_pumps-pumps+1) is equal to 1 - 1/(maximal_pumps-pumps+1)
	  //and the probability that BurstProb < 1/(maximal_pumps-pumps+1) is equal to 1/(maximal_pumps-pumps+1)
	  //In other words, the ballon will burst with probability 1/(maximal_pumps-pumps+1), and will not burst with probability 1-1/(maximal_pumps-pumps+1)
      if (BurstProb > 1/(maximal_pumps-pumps+1)) {
	size +=increase;
	$('#ballon').width(size); 
        $('#ballon').height(size);
		show_present();
		show_present_earns();
      }
      else {
	last_win = 0;
	pumpmeup = pumps;
	pumps = -1; // makes pumping button unclickable until new round starts
	explosion = 1; // save that balloon has exploded this round
	balloon_explode();
	exploded.push(explosion); // save whether balloon has exploded or not
	number_pumps.push(pumpmeup); // save number of pumps
	 $('#ballon').hide();
	$('#present_round').hide();
    setTimeout(explosion_message, 1200);
	setTimeout(gonext_message, 1200);
	setTimeout(show_last, 1200);
      }
    }
  });
  
  
  // collect button: release pressure and hope for money
  $('#collect').click(function() {
      if (pumps === 0) {
	alert('You can only collect the money once you click "Inflate balloon”.');
      }
      else if (pumps > 0) { // only works after at least one pump has been made
	exploded.push(explosion); // save whether balloon has exploded or not
	document.getElementById('tada_sound').play();
	number_pumps.push(pumps); // save number of pumps
	pumpmeup = pumps;
	pumps = -1; // makes pumping button unclickable until new round starts
	$('#ballon').hide();
	$('#present_round').hide();
	collected_message();
	gonext_message();
	total += present_win;
	last_win = present_win;
	increase_value();
	show_last();
      }
  });
  
  // click this button to start the next round (or end game when all rounds are played)
  $('#gonext').click(function() {
    if (round < rounds_played) {
      new_round();
    }
    else {
      end_game();
    }
  });  


  // start the game!
  new_round();
  
});

});

Qualtrics.SurveyEngine.addOnReady(function()
{
	/*Place your JavaScript here to run when the page is fully displayed*/

});

Qualtrics.SurveyEngine.addOnUnload(function()
{
	/*Place your JavaScript here to run when the page is unloaded*/

});
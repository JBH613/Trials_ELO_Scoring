# Trials_ELO_Scoring
<!doctype html> 
 <script  src="https://code.jquery.com/jquery-2.2.4.min.js"></script>
 <link href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.6/css/bootstrap.min.css" rel="stylesheet">
  <style>
	body { padding-top:2rem; }
	input{ width:80px; }
	td,th{ text-align:center; }
	thead th { text-align:left; }
  </style>
<body>  
<div class=container>
  
 <table class="table table-bordered players">
 <thead class="thead-inverse">
    <tr>
      <th colspan=4>Your Team Elo</th>
    </tr>
  </thead>
	 <tr>
		<th>Player 1</th>
		<th>Player 2</th>
		<th>Player 3</th>
		<th>Average</th>
	 </tr>
	 <tr>
		<td><input type=text value="1600"></td>
		<td><input type=text value="1900"></td>
		<td><input type=text value="1105"></td>
		<td><div class=average></div></td>
	 </tr>
</table>



<table class="table table-bordered players">
 <thead class="thead-inverse">
    <tr>
      <th colspan=4>Enemy Team Elo</th>
    </tr>
  </thead>
	 <tr>
		<th>Player 1</th>
		<th>Player 2</th>
		<th>Player 3</th>
		<th>Average</th>
	 </tr>
	 <tr>
		<td><input type=text value="1000"></td>
		<td><input type=text value="1400"></td>
		<td><input type=text value="1100"></td>
		<td><div class=average></div></td>
	 </tr>
</table>


<ul>
<li>Spread:	<span id=spread></li>
<li>Win %:	<span id=winpercent></li>
<li>Win points:	<span id=winpoints></li>
<li>Lose points:	<span id=losepoints></li>
</ul>
</div>
</body>

<script>
	function recalc()
	{
		var sum1 = 0, count1 = 0;
		
		$('table.players').first().find('input').each(function() {
			var v = parseInt(this.value);
			if (!isNaN(v)) {
				sum1 += v;
				count1++;
			}
		});
		var sum2 = 0, count2=0;
		$('table.players').last().find('input').each(function() {
			var v = parseInt(this.value);
			if (!isNaN(v)) {
				sum2 += v;
				count2++;
			}
		});
		
		$('table.players').first().find('.average').html(parseInt(sum1/count1));
		$('table.players').last().find('.average').html(parseInt(sum2/count2));
	
		var spread = (sum1/count1) - (sum2/count2);
		$('#spread').html(parseInt(spread));
		console.log(spread/400);
		var percent = (100.0/(1+Math.pow(10, -1 * spread/400.0))).toFixed(2);
		$('#winpercent').html(percent + '%');
		
		
		var winPoints = '?', losePoints = '?';
		if (spread >= 401)	{	winPoints = 0; losePoints = 15; 	}
		else if (spread >= 351)	{	winPoints = 1; losePoints = -15; 	}
		else if (spread >= 301)	{	winPoints = 2; losePoints = -14; 	}
		else if (spread >= 251)	{	winPoints = 3; losePoints = -13; 	}
		else if (spread >= 201)	{	winPoints = 4; losePoints = -12; 	}
		else if (spread >= 151)	{	winPoints = 5; losePoints = -11; 	}
		else if (spread >= 101)	{	winPoints = 6; losePoints = -10; 	}
		else if (spread >= 51)	{	winPoints = 7; losePoints = -9; 	}
		else if (spread >= 0)	{	winPoints = 8; losePoints = -8; 	}
		else if (spread >= -50)	{	winPoints = 8; losePoints = -8; 	}
		else if (spread >= -100)	{	winPoints = 9; losePoints = -8; 	}
		else if (spread >= -150)	{	winPoints = 10; losePoints = -6; 	}
		else if (spread >= -200)	{	winPoints = 11; losePoints = -5; 	}
		else if (spread >= -250)	{	winPoints = 12; losePoints = -4; 	}
		else if (spread >= -300)	{	winPoints = 13; losePoints = -3; 	}
		else if (spread >= -350)	{	winPoints = 14; losePoints = -2; 	}
		else if (spread >= -400)	{	winPoints = 15; losePoints = -1; 	}
		else 	{	winPoints = 15; losePoints = -1; 	}
		
		
		$('#winpoints').html(winPoints);
		$('#losepoints').html(losePoints);
	}
	
	
	$(function() {
		$('input').on('keyup', recalc);
		recalc();
	});
</script>

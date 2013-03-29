<?php
if(!isset($_POST['submit'])){
        ?>
        <html>
        <body>
                <h1>Elevation Leaderboard</h1>
                <form method="post" action="<?php echo $_SERVER['PHP_SELF'];?>">
		<p>
		Please enter a club name to see the elevation leaderboard for this month
		</p>
		Name: <input type="text" name="club" size="55" placeholder="i.e. Team Every Man Jack, cal tri, TEAM STRAVA, etc.">
		<br/><br/>
                <input type="submit"  value="Go" name="submit"/>
		<small>This may take a while for larger clubs</small>
                <form/>
        <body/>
        <html/>
<?php
} else {
	#some constants
	$v1_base_url = 'http://app.strava.com/api/v1';
	$v2_base_url = 'http://www.strava.com/api/v2';
	$this_month = date("Y-m");
	$date_regex = "/".$this_month.".*/";

	#get id and name for club
	$club_string = str_replace(' ', '%20', strtolower($_POST["club"]));
	$club_url = $v1_base_url . '/clubs?name='.$club_string;
	$club_data = json_decode(file_get_contents($club_url));

	$offset = 0;
	$riders_list = array(0);
	$members = array(0);
	$clubs = $club_data->{'clubs'}[0];
	if (count($clubs) == 0) {
		echo "<h2>No clubs found with the given name. Please try again.</h2>";
		?><br/><a href="/st/">Back</a><?php
	} else if (count($clubs) > 1) {
		echo "<h2>Multiple clubs found. Please try again.</h2>";
		?><br/><a href="/st/">Back</a><?php
	} else {

		$club_name = $club_data->{'clubs'}[0]->{'name'};
		$club_id = $club_data->{'clubs'}[0]->{'id'};

		#get club members
		do {
			if ($offset  == 0) {
				$members_url = $v1_base_url.'/clubs/'.$club_id.'/members';
			} else {
				$members_url = $v1_base_url.'/clubs/'.$club_id.'/members'.'&offset='.$offset;
			}
			$members_data = json_decode(file_get_contents($members_url));
			$members = array_merge($members, $members_data->{'members'});
			$offset += 50;
		} while (count($members) % 50 == 0 && $offset < count($members+51));

		#iterate over members to calculate ride data
		foreach ($members as $member) {
			$member_id = $member->{'id'};
			$member_name = $member->{'name'};
			$tot_elevation = 0;
			$num_rides = 0;

			$rides_url = $v1_base_url.'/rides?athleteId='.$member_id;
			$rides = json_decode(file_get_contents($rides_url))->{'rides'};

			#iterate over rides to collect data
			foreach ($rides as $ride) {
				$ride_id = $ride->{'id'};
				$ride_url = $v2_base_url.'/rides/'.$ride_id;
				$ride_data = json_decode(file_get_contents($ride_url))->{'ride'};
				if (preg_match($date_regex, $ride_data->{'start_date_local'})) {
					$num_rides++;
					$tot_elevation += $ride_data->{'elevation_gain'};
				}
				/*here I would check to see if the member did more than 50 rides in this month and add elevation and number of rides to it (for simplicity, I assumed no one rides more than 50 times in one month)*/
			}
			if ($num_rides == 0) { #prevent divide by zero
				$avg_elevation = 0;
			} else {
				$avg_elevation = $tot_elevation / $num_rides;
			}
			$rider = array('tot_elevation' => $tot_elevation, 'name' => $member_name, 'num_rides' => $num_rides, 'avg_elevation' => $avg_elevation);
			$riders_list[] = $rider;
		}
		rsort($riders_list); #sort array by tot_elevation

		#print the leaderboard
		$pos = 1;
		echo "<h1>$club_name Leaderboard for $this_month</h1>";
		echo '<table>';
		echo '<tr>';
		echo "<td><h2>Ranking&#160</h2></td>";
		echo "<td><h2>Name&#160</h2></td>";
		echo "<td><h2>Total Elevation(m)&#160</h2></td>";
		echo "<td><h2>Number of rides&#160</h2></td>";
		echo "<td><h2>Average elevation/ride(m)</h2></td>";
		echo '</tr>';
		foreach($riders_list as $rider) {
			if ($rider['name'] != "") {
				echo '<tr>';
				echo "<td>$pos.</td>";
				echo "<td>{$rider['name']}&#160</td>";
				echo "<td>".number_format($rider['tot_elevation'],0)."&#160</td>";
				echo "<td>{$rider['num_rides']}&#160</td>";
				echo "<td>".number_format($rider['avg_elevation'], 0)."&#160</td>";
				echo '</tr>';
				$pos++;
			}
		}
		echo '</table>';
	}
}
?>

<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Live Cricket Scoreboard</title>
    <style>
        body {
            background: #0a0a0a;
            color: white;
            font-family: Arial, sans-serif;
            padding: 20px;
        }
        .score-box {
            background: #111;
            padding: 18px;
            border-radius: 10px;
            width: 95%;
            margin: auto;
            box-shadow: 0px 0px 15px #00ffe1;
        }
        .team {
            font-size: 26px;
            font-weight: bold;
            color: #00eaff;
        }
        .runs {
            font-size: 40px;
            font-weight: bold;
            margin-top: 8px;
        }
        .info {
            font-size: 18px;
            margin-top: 5px;
        }
        .sub-box {
            margin-top: 20px;
            background: #1a1a1a;
            padding: 10px;
            border-radius: 10px;
        }
    </style>
</head>

<body>
    <h2>🔴 Live Cricket Score</h2>

    <div class="score-box">
        <div id="team" class="team">Loading...</div>
        <div id="score" class="runs">--/--</div>
        <div id="overs" class="info">Overs: --</div>

        <div class="sub-box">
            <div id="batsmen" class="info">Batsmen: Loading...</div>
            <div id="bowler" class="info">Bowler: Loading...</div>
            <div id="partnership" class="info">Partnership: --</div>
        </div>
    </div>

<script>
const MATCH_ID = "56933";  // যেকোনো ম্যাচ ID দিতে পারো Cricbuzz লিংক থেকে

async function loadScore() {
    try {
        let api = `https://cricbuzz-api.vercel.app/cricket-score?matchId=${MATCH_ID}`;
        let res = await fetch(api);
        let data = await res.json();

        document.getElementById("team").innerHTML = data.team1 + " vs " + data.team2;
        document.getElementById("score").innerHTML = data.score;
        document.getElementById("overs").innerHTML = "Overs: " + data.overs;
        document.getElementById("batsmen").innerHTML =
            "Batsmen: " + data.batsman1 + " (" + data.b1_runs + ") & " + data.batsman2 + " (" + data.b2_runs + ")";
        document.getElementById("bowler").innerHTML =
            "Bowler: " + data.bowler + " – " + data.bowler_overs + " overs";
        document.getElementById("partnership").innerHTML = "Partnership: " + data.partnership;

    } catch (e) {
        document.getElementById("team").innerHTML = "Error loading score";
    }
}

loadScore();
setInterval(loadScore, 10000);
</script>

</body>
</html>
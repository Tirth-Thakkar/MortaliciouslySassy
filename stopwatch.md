<html>
<head>
	<title>Stopwatch</title>
	<style>
		.container {
			display: flex;
			flex-direction: column;
			align-items: center;
		}
		.timer {
			font-size: 5rem;
			margin-bottom: 2rem;
		}
		.buttons {
			display: flex;
			flex-direction: row;
		}
		.button {
			font-size: 1.5rem;
			margin: 0 0.5rem;
			padding: 0.5rem 1rem;
			border-radius: 0.5rem;
			background-color: #007bff;
			color: #fff;
			cursor: pointer;
		}
	</style>
</head>
<body>
	<div class="container">
		<div class="timer">00:00:00</div>
		<div class="buttons">
			<button id="startButton" class="button">Start</button>
			<button id="stopButton" class="button">Stop</button>
			<button id="resetButton" class="button">Reset</button>
		</div>
	</div>
	<script>
		let timer = document.querySelector(".timer");
		let startButton = document.querySelector("#startButton");
		let stopButton = document.querySelector("#stopButton");
		let resetButton = document.querySelector("#resetButton");
		let startTime = 0;
		let elapsedTime = 0;
		let timerInterval;
		function updateTimer() {
			let currentTime = new Date().getTime();
			elapsedTime = currentTime - startTime;
			let hours = Math.floor(elapsedTime / 3600000);
			let minutes = Math.floor((elapsedTime % 3600000) / 60000);
			let seconds = Math.floor((elapsedTime % 60000) / 1000);
			let milliseconds = elapsedTime % 1000;
			timer.innerHTML = `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}.${milliseconds.toString().padStart(3, '0')}`;
		}
		function startTimer() {
			startButton.disabled = true;
			stopButton.disabled = false;
			resetButton.disabled = true;
			startTime = new Date().getTime() - elapsedTime;
			timerInterval = setInterval(updateTimer, 10);
		}
		function stopTimer() {
			startButton.disabled = false;
			stopButton.disabled = true;
			resetButton.disabled = false;
			clearInterval(timerInterval);
		}
		function resetTimer() {
			startButton.disabled = false;
			stopButton.disabled = true;
			resetButton.disabled = true;
			clearInterval(timerInterval);
			elapsedTime = 0;
			updateTimer();
		}
		startButton.addEventListener("click", startTimer);
		stopButton.addEventListener("click", stopTimer);
		resetButton.addEventListener("click", resetTimer);
	</script>
</body>
</html>

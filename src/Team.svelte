<script>
	export let name
	export let doubles

	let scores = []
	let doublesScores = []
	let addingTo = 0
	$: if (!doubles) {
		doublesScores = []
		addingTo = 0
	}

	let timeout1 = false
	let timeout2 = false
	let timeout3 = false

	$: totalScore = scores.length + doublesScores.length
	$: aces = scores.filter(score => score === "A").length + doublesScores.filter(score => score === "A").length
	$: kills = scores.filter(score => score === "K").length + doublesScores.filter(score => score === "K").length

	function add(score) {
		if (addingTo == 1) doublesScores = [...doublesScores, score]
		else scores = [...scores, score]
	}
</script>

<div>
	<h3>{name} Team</h3>
	Timeouts:
	<button
		class={timeout1 ? "disabled" : "enabled"}
		disabled={timeout1}
		on:click={() => timeout1 = true}
	>
		1
	</button>
	<button
		class={timeout2 ? "disabled" : "enabled"}
		disabled={timeout2}
		on:click={() => timeout2 = true}
	>
		2
	</button>
	<button
		class={timeout3 ? "disabled" : "enabled"}
		disabled={timeout3}
		on:click={() => timeout3 = true}
	>
		3
	</button>
	<br>
	<div id="container">
		{#if doubles}
			<div id="dbuttons">
				<button on:click={() => {addingTo = 0}} class={addingTo == 0 ? "black" : "white"}></button>
				<button on:click={() => {addingTo = 1}} class={addingTo == 1 ? "black" : "white"}></button>
			</div>
		{/if}
		<div id="buttons">
			<button on:click={() => add("✓")}>✓</button><br>
			<button on:click={() => add("A")}>A</button><br>
			<button on:click={() => add("K")}>K</button>
		</div>
		<div class="scoresContainer">
			<div class="scores">
				{#each scores.length > doublesScores.length ? scores : doublesScores as score, i}
					<span class="box noborder">{i+1}</span>
				{/each}
			</div>
			<div class="scores">
				{#each scores as score, i}
					<span class="box border">{score}</span>
				{/each}
			</div>
			<div class="scores">
				{#each doublesScores as score, i}
					<span class={"box border" + (i >= scores.length ? " readd" : "")}>{score}</span>
				{/each}
			</div>
		</div>
	</div>
	<div id="scores">
		<p>Total Score: {totalScore}</p>
		<p>Aces: {aces}</p>
		<p>Kills: {kills}</p>
	</div>
</div>

<style>
	.disabled {
		background-color: black;
		color: white;
	}
	#container, .scores {
		display: flex;
	}
	#container > * {
		margin-left: 3px;
		margin-right: 3px;
	}
	.box, .scoresContainer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		text-align: center;
	}
	.box {
		width: 3ch;
		height: 3ch;
	}
	.border {
		border: 1px solid black;
	}
	.noborder {
		border: 1px solid rgba(0, 0, 0, 0); /* make things in line when a bunch are in a row */
	}
	.scores:nth-child(3) .border:not(.readd) {
		border-top: none;
	}
	.box:not(:nth-child(1)) {
		border-left: none;
	}
	#buttons button, #dbuttons button {
		min-width: 3ch;
	}
	#dbuttons {
		display: flex;
		flex-direction: column;
	}
	#dbuttons button {
		flex-grow: 1;
	}
	.black {
		background-color: black;
	}
</style>

<script>
	import Team from "./Team.svelte";

	let doubles = true;
</script>

<main>
	<div id="main">
		<h1>Handball Scoring</h1>
		<button on:click={() => doubles = !doubles}>
			{doubles ? "Switch to Singles" : "Switch to Doubles"}
		</button>
		<div id="container">
			<div class="team">
				<Team name={"Home"} {doubles}></Team>
			</div>
			<div class="team">
				<Team name={"Away"} {doubles}></Team>
			</div>
		</div>
	</div>
</main>

<style>
	h1 {
		/*text-align: center;*/
	}
	#container {
		display: flex;
		flex-direction: column;
	}
	.team {
		margin-left: 5px;
		margin-right: 5px;
	}
	main {
		display: flex;
		/*align-items: center;
		justify-content: center;*/
	}
</style>

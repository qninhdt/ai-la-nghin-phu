<script>
	import NavBar from '../components/NavBar.svelte';

	export let segment;
</script>

<style>
	
	main {
		position: relative;
		max-width: 56em;
		background-color: white;
		padding: 2em;
		margin: 0 auto;
		box-sizing: border-box;
	}

	.author {
		color: rgb(201, 201, 201);
		text-align: end;
		padding-right: 10px;
		font-size: 10px;
	}

	.author span {
		color: #00d8b8;
		font-weight: 600;
	}

</style>

<svelte:head>
	<title>Ai là "nghìn" phú :u</title>
</svelte:head>

<NavBar {segment}/>

<main>
	<slot></slot>
</main>
<footer>
	<div class="author"><i>Design by <span>lema0</span></i></div>
</footer>
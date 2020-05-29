
<script>
	let kit = "1"
	
	$: gameLink = "/play/" + kit
</script>

<style>
	#username-input {
		text-align: center;
	}
	#username-input::placeholder {
		text-align: center;
	}
	#game-home {
		text-align: center;
	}
	#game-title {
		font-family: monospace;
		text-align: center;
		margin: 80px 0px 50px;
	}
	#game-title span {
		color: #00bda0;
		font-weight: 900;
	}
	#play-button {
		margin: 50px;
	}
	#game-logo {
		height: 200px;
		width: 200px;
		margin: auto;
	}
</style>

<div id="game-home" class="container">

	<figure id="game-logo" class="image">
		<img alt="money" src="money.svg">
	</figure>

	<h1 id="game-title" class="title is-1">Ai là <span>"nghìn"</span> phú ??</h1>

	<p class="select" style="margin-bottom: 20px">
		<select bind:value={kit}>
			<option value="1">Bộ câu hỏi 1</option>
			<option value="2">Bộ câu hỏi 2</option>
		</select>
	</p>

	<p class="control has-icons-left has-icons-right">
		<input id="username-input" class="input is-large" type="text" name="username" autocomplete="off" placeholder="Nhập tên ..."/>
		<span class="icon is-small is-left">
			<i class="fas fa-dollar-sign"></i>
		</span>
		<span class="icon is-small is-right">
			<i class="fas fa-dollar-sign"></i>
		</span>
	</p>

	<a href={gameLink} id="play-button" class="button is-primary is-large">
		<span class="icon is-large">
		<i class="fas fa-play"></i>
		</span>
		<b>CHƠI</b>
	</a>
</div>
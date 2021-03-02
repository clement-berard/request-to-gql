<script>
	export let name;

	function handleClick() {
		// const to = getFileContent('./input.txt');
		const regex = /(--data-raw)(.)+/gm;
		const found = to.match(regex)[0];
		const t1 = found.substring(12)
		const t2 = t1.slice(0, -3)
		const {variables, query} = JSON.parse(t2)
		console.log('variables', variables);
		console.log(query);
	}
</script>

<main>
	<h1>Hello</h1>
	<textarea class="input-code-curl"/>
	<div class="result">
		<div class="variables">
			fdsafd
		</div>
	</div>
</main>

<style type="text/scss">
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;

		textarea.input-code-curl {
			width: 60vw;
			height: 400px;
		}
		.result {
			.variables {
				background-color: blue;
			}
		}
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>

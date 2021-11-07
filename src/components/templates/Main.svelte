<script>
	import Text from "$atoms/Text.svelte";
	import Button from "$atoms/Button.svelte";
	import NumberInput from "$atoms/NumberInput.svelte";
	import Icon from "$atoms/Icon.svelte";
	// @ts-ignore
	import ThemeContext from "$atoms/ThemeContext.svelte";
	let answer;
	function mul(x, y) {
		console.log(x, y);
		var p = [];
		while (y > 0) {
			p.push([x, y]);
			x = x * 2;
			y = Math.floor(y / 2);
			console.log(x, y);
		}
		console.log(p);
		return p;
	}
	let left, right;

	function calculate() {
		answer = mul(left, right);
	}
	// let themeName;
	// onMount(async () => {
	// 	localStorage.getItem("key") &&
	// 		login(JSON.parse(localStorage.getItem("key")));
	// });
</script>

<ThemeContext>
	<div
		class="  overflow-auto py-7 w-full h-screen px-2  flex flex-col bg-background  items-center "
	>
		<div>
			<Text type=" title ">Ethiopian Multiplication</Text>
		</div>
		<Text type=" body  "
			>This is a demonstration of An ancient ethiopian method for
			multiplying numbers.</Text
		>

		<div class="w-full  mt-2 flex flex-col justify-center items-center">
			<div
				class=" w-3/4 px-10 flex py-5 flex-col sm:flex-row space-y-5 sm:space-y-0 sm:space-x-5 justify-center items-center"
			>
				<NumberInput placeholder="Number 1" bind:value={left} />
				<Icon name="close" />
				<NumberInput placeholder="Number 2" bind:value={right} />
			</div>
		</div>
		<Button
			on:click={calculate}
			variant="primary"
			left="fire"
			name="Calculate"
		/>
		{#if answer}
			<div
				class=" my-5 w-full sm:w-1/2 px-2 flex flex-col justify-center items-center bg-surface rounded-lg"
			>
				<div
					class="w-full flex flex-row px-4 rounded-lg justify-around"
				>
					<Text type=" title ">x2</Text>
					<Text type=" title ">/2</Text>
				</div>
				{#each answer as house}
					<div
						class="{house[1] % 2 != 0
							? 'bg-success/20'
							: 'bg-error/20'} w-full flex flex-row px-4 py-2 my-2 rounded-lg justify-around"
					>
						<Text type=" body text-on-background">
							{house[0]}
						</Text>
						<Text type=" body text-on-background">
							{house[1]}
						</Text>
					</div>
				{/each}
				<Text type=" title ">
					{answer
						.filter((a) => a[1] % 2 != 0)
						.map((x) => x[0])
						.reduce((a, b) => a + b, 0)}
				</Text>
			</div>
		{/if}
		<Text class="pt-4" type=" body ">
			More info about the algorithm and the story goes here...
		</Text>
	</div>
</ThemeContext>

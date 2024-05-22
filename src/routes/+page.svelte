<script>
	import Stamp from '$lib/components/Stamp.svelte';
	import Controllers from '$lib/components/Controllers.svelte';

	let rgbColor;
	let text1;
	let text2;
	let text3;
	let radius;
	let adjustHue;
	let drawText;

</script>

<svelte:head>
	<title>Stamp Gen</title>
	<meta name="description" content="Free StampJam Clone" />
</svelte:head>

<div class="wrapper flex justify-between">

<div class="stamp">
	<Stamp 
		bind:rgbColor 
		bind:radius 
		bind:adjustHue 
		bind:drawText 
		bind:text1
		bind:text2
		bind:text3
		/>
</div>
<div class="controllers">
	<Controllers 
		bind:text1
		bind:text2
		bind:text3
		bind:rgbColor 
		bind:radius
		bind:adjustHue
		bind:drawText
		/>
</div>
</div>

<style>

	@media only screen and (max-width: 700px) {
  		.wrapper {
  		  display: block !important;
		  text-align: center;
  		}
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>

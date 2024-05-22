<script>
	import { onMount } from "svelte";
	import { browser } from "$app/environment";
	import domtoimage from "dom-to-image";
	import CircleType from 'circletype';
	//import {ColorChange} from "$lib/color-change"
	
	let imageSource = "/templates/1.png";
	export let rgbColor = "rgba(255,255,255,1)";
	export let radius = 140;
	export let text1 = "★★CORPORATE SEAL★★";
	export let text2 = "YOUR COMPANY NAME";
	export let text3 = "EST. 2021";


	let circleType1;
	let circleType2;

	export function drawText() {
		if (circleType1) {
				console.log(circleType1)
				circleType1.destroy(circleType1)
				document.getElementById('text1').innerText = text1;
			}

			circleType1 = new CircleType(document.getElementById('text1'));

			// Set the text radius and direction. Note: setter methods are chainable.
			circleType1.radius(radius);

			if (circleType2) {
				console.log(circleType2)
				circleType2.destroy(circleType2)
				document.getElementById('text3').innerText = text3;
			}

			circleType2 = new CircleType(document.getElementById('text3'));

			// Set the text radius and direction. Note: setter methods are chainable.
			circleType2.dir(-1).radius(150);
	}

	// Function to adjust hue of the image stroke
	export function adjustHue() {
		
		// if (browser) {
		// 	console.log('Hue adjusted: ', rgbColor)
		// 	// Select the element you want to change
		// 	let cc = new ColorChange('#stampImage')

		// 	// Change the color & hue of the element into 'red'
		// 	cc.setColor('#0EDAB6')
		// }

		if (browser) {
			drawText();

			const canvas = document.getElementById("canvas");
			const ctx = canvas.getContext("2d");

			const img = new Image();
			img.onload = function () {
				canvas.width = img.width;
				canvas.height = img.height;

				// draw rgbColor
				ctx.fillStyle = rgbColor;
				ctx.fillRect(0, 0, img.width, img.height);

				// set composite mode
				ctx.globalCompositeOperation = "destination-in";
				// Draw the image
				ctx.drawImage(img, 0, 0);

				//ctx.font = "100px Arial";
				//ctx.fillText(text1,10,80);
			};
			img.src = imageSource;
		}
	}

	// Function to download the canvas as PNG
	function downloadCanvas() {
		//   const canvas = document.getElementById('canvas');
		//   const link = document.createElement('a');
		//   link.download = 'image.png';
		//   link.href = canvas.toDataURL();
		//   link.click();

		var node = document.getElementById("stamp");

		domtoimage
			.toPng(node)
			.then(function (dataUrl) {
				var img = new Image();
				img.src = dataUrl;
				document.body.appendChild(img);
			})
			.catch(function (error) {
				console.error("oops, something went wrong!", error);
			});

		domtoimage
			.toBlob(document.getElementById("stamp"))
			.then(function (blob) {
				var url = URL.createObjectURL(blob);
        		var link = document.createElement('a');
        		link.href = url;
        		link.download = 'image.png';
        		document.body.appendChild(link);
        		link.click();
        		document.body.removeChild(link);
        		URL.revokeObjectURL(url);
			});
	}

	$: rgbColor, adjustHue();

	// Load the image source on component mount
	onMount(() => {
		adjustHue();
		drawText();
	});
</script>

<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=Lexend+Mega:wght@100..900&display=swap" rel="stylesheet">

</svelte:head>

<div id="stamp">
	<canvas class="w-full" id="canvas">
	</canvas>
	<span 
		style="color: {rgbColor}"
		id="text1">{text1}</span>

		<span 
		style="color: {rgbColor}"
		id="text2">{text2}</span>

		<span 
		style="color: {rgbColor}"
		id="text3">{text3}</span>
</div>

<!-- <div id="stamp">
	<img class="stampImage" src="/templates/1.png" alt="stamp" />
	<span class="text1">{text1}</span>
</div> -->

<button
	on:click={downloadCanvas}
	class="group m-5 text-center relative h-12 w-48 overflow-hidden rounded-lg bg-white text-lg shadow"
>
	<div
		class="absolute inset-0 w-3 bg-indigo-500 transition-all duration-[250ms] ease-out group-hover:w-full"
	></div>
	<span class="relative text-black group-hover:text-white">Download</span>
</button>

<style>
	/* Add your CSS styles here */
	canvas {
		text-align: center;
		border: solid 1px #8e8e8e;
		padding: 2rem;
	}
	#stamp {
		position: relative;
		min-width: 400px;
		max-width: 400px;
	}
	#stamp #text1 {
		position: absolute;
		font-size: 1.7rem;
		top: 60px;
		right: 199px;
		font-family: "Lexend Mega", sans-serif;
	}
	#stamp #text2 {
		position: absolute;
		font-size: 1.7rem;
		top: 150px;
		right: 109px;
		line-height: normal;
		font-weight: 500;
		width: 181px;
		font-family: "Lexend Mega", sans-serif;
		text-align: center;
	}
	#stamp #text3 {
		position: absolute;
		font-size: 1.7rem;
		bottom: 70px;
		right: 199px;
		font-family: "Lexend Mega", sans-serif;
	}
</style>

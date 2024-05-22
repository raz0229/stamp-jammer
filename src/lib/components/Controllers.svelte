<script>
    import HsvPicker from "$lib/components/HsvPicker.svelte";

    export let rgbColor;
    export let text1;
    export let text2;
    export let text3;
    export let radius;
    export let adjustHue;
    export let drawText;

    function colorCallback(rgba) {
        const { r, g, b, a } = rgba.detail;

        rgbColor = `rgba(${r},${g},${b},${a})`;
    }

    function addTextToCanvas(text, x, y) {
        // Get the canvas element
        const canvas = document.getElementById("canvas");
        if (!canvas) {
            console.error("Canvas element not found");
            return;
        }

        // Get the 2D drawing context
        const context = canvas.getContext("2d");
        if (!context) {
            console.error("2D context not available");
            return;
        }

         // Save the current globalCompositeOperation
        const previousCompositeOperation = context.globalCompositeOperation;

         // Temporarily set globalCompositeOperation to 'source-over' to draw the text
        context.globalCompositeOperation = 'source-over';

        // Set font style (optional)
        context.font = "2rem Arial";

        // Set fill style (optional)
        context.fillStyle = rgbColor;

        // Draw the text at the specified position
        context.fillText(text, x, y);

        // Restore the original globalCompositeOperation
        context.globalCompositeOperation = previousCompositeOperation;
    }

    const editText1 = () => {
        console.log('Adding text1 at [10,20] : ', text1)
        //addTextToCanvas(text1, 10, 20);
        drawText();
    }

    const editText2 = () => {
        //addTextToCanvas(text2, 10, 50);
    }

    const editText3 = () => {
        //addTextToCanvas(text3, 10, 70);
        console.log(text3)
        drawText();
    }

    const radiusChanged = () => {
        console.log(radius)
        adjustHue();
    }

</script>

<div class="max-w-2xl mx-auto">
    <div class="m-2">
        <div class="flex">
            <span
                class="inline-flex items-center px-3 text-sm text-gray-900 bg-gray-200 border border-r-0 border-gray-300 rounded-l-md dark:bg-gray-600 dark:text-gray-400 dark:border-gray-600"
            >
                1️⃣
            </span>
            <input
                on:change={editText1}
                bind:value={text1}
                type="text"
                id="website-admin"
                class="rounded-none rounded-r-lg bg-gray-50 border text-gray-900 focus:ring-blue-500 focus:border-blue-500 block flex-1 min-w-0 w-full text-sm border-gray-300 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="Text 1"
            />
        </div>
    </div>
    <div class="m-2">
        <div class="flex">
            <span
                class="inline-flex items-center px-3 text-sm text-gray-900 bg-gray-200 border border-r-0 border-gray-300 rounded-l-md dark:bg-gray-600 dark:text-gray-400 dark:border-gray-600"
            >
                2️⃣
            </span>
            <input
                on:change={editText2}
                bind:value={text2}
                type="text"
                id="website-admin"
                class="rounded-none rounded-r-lg bg-gray-50 border text-gray-900 focus:ring-blue-500 focus:border-blue-500 block flex-1 min-w-0 w-full text-sm border-gray-300 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="Text 2"
            />
        </div>
    </div>
    <div class="m-2">
        <div class="flex">
            <span
                class="inline-flex items-center px-3 text-sm text-gray-900 bg-gray-200 border border-r-0 border-gray-300 rounded-l-md dark:bg-gray-600 dark:text-gray-400 dark:border-gray-600"
            >
                3️⃣
            </span>
            <input
                bind:value={text3}
                on:change={editText3}
                type="text"
                id="website-admin"
                class="rounded-none rounded-r-lg bg-gray-50 border text-gray-900 focus:ring-blue-500 focus:border-blue-500 block flex-1 min-w-0 w-full text-sm border-gray-300 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="Text 3"
            />
        </div>
    </div>

    <div class="m-2">
        <div class="flex">
            <span
                class="inline-flex items-center px-3 text-sm text-gray-900 bg-gray-200 border border-r-0 border-gray-300 rounded-l-md dark:bg-gray-600 dark:text-gray-400 dark:border-gray-600"
            >
                R
            </span>
            <input
                bind:value={radius}
                on:change={radiusChanged}
                type="number"
                id="website-admin"
                class="rounded-none rounded-r-lg bg-gray-50 border text-gray-900 focus:ring-blue-500 focus:border-blue-500 block flex-1 min-w-0 w-full text-sm border-gray-300 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="Radius"
            />
        </div>
    </div>

    <div class="color-picker mt-4">
        <HsvPicker on:colorChange={colorCallback} startColor={"#FBFBFB"} />
    </div>

    <script src="https://unpkg.com/flowbite@1.4.0/dist/flowbite.js"></script>
</div>

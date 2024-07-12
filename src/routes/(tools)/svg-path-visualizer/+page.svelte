<script>
    import { onMount } from 'svelte';

    let pathInput = '';
    let svgPathDescription = '';

    const updateSVG = () => {
        const svgCanvas = document.getElementById('svgCanvas');
        svgCanvas.innerHTML = '';

        const newPath = document.createElementNS('http://www.w3.org/2000/svg', 'path');
        newPath.setAttribute('d', pathInput);
        newPath.setAttribute('stroke', 'black');
        newPath.setAttribute('stroke-width', '2');
        newPath.setAttribute('fill', 'none');

        svgCanvas.appendChild(newPath);
        describePath();
    };

    const describePath = () => {
        const commands = pathInput.match(/[a-z][^a-z]*/ig);
        if (commands) {
            svgPathDescription = commands.map(command => {
                const type = command.charAt(0).toUpperCase();
                const values = command.slice(1).trim().split(/[ ,]/).map(val => parseFloat(val)).join(', ');
                const description = getDescription(type, values);
                return `Command: ${type}\nValues: [${values}]\nDescription: ${description}`;
            }).join('\n\n');
        } else {
            svgPathDescription = 'Invalid SVG path.';
        }
    };

    const getDescription = (type, values) => {
        switch(type) {
            case 'M':
                return `Move to the starting point (${values[0]}, ${values[1]}).`;
            case 'L':
                return `Draw a line to the point (${values[0]}, ${values[1]}).`;
            case 'H':
                return `Draw a horizontal line to x = ${values[0]}.`;
            case 'V':
                return `Draw a vertical line to y = ${values[0]}.`;
            case 'C':
                return `Draw a cubic Bezier curve to the point (${values[4]}, ${values[5]}) with control points (${values[0]}, ${values[1]}) and (${values[2]}, ${values[3]}).`;
            case 'S':
                return `Draw a smooth cubic Bezier curve to the point (${values[2]}, ${values[3]}) with control point (${values[0]}, ${values[1]}).`;
            case 'Q':
                return `Draw a quadratic Bezier curve to the point (${values[2]}, ${values[3]}) with control point (${values[0]}, ${values[1]}).`;
            case 'T':
                return `Draw a smooth quadratic Bezier curve to the point (${values[0]}, ${values[1]}).`;
            case 'A':
                return `Draw an elliptical arc to the point (${values[5]}, ${values[6]}) with radii (${values[0]}, ${values[1]}), rotation ${values[2]}, large-arc-flag ${values[3]}, and sweep-flag ${values[4]}.`;
            case 'Z':
                return `Close the path by drawing a straight line back to the starting point.`;
            default:
                return `Unknown command.`;
        }
    };
</script>

<style>
    #svgCanvas {
        width: 100%;
        height: 400px;
        border: 1px solid black;
        background-color: white;
    }

    pre {
        background: #f4f4f4;
        padding: 1em;
        border-radius: 4px;
        text-align: left;
        white-space: pre-wrap;
        word-wrap: break-word;
    }
</style>

<main class="container mx-auto p-4">
    <div class="mb-4">
        <label for="pathInput" class="block mb-2 text-2xl font-medium text-gray-500">Enter SVG Path:</label>
        <input type="text" id="pathInput" bind:value={pathInput} placeholder="M10 10 H 90 V 90 H 10 L 10 10" class="w-full p-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
    </div>
    <div class="flex justify-center mb-4">
        <button on:click={updateSVG} class="bg-blue-500 text-white py-2 px-4 rounded-md hover:bg-blue-600 transition">Visualize</button>
    </div>
    
    <div class="mt-6 flex justify-center">
        <svg id="svgCanvas" class="w-full max-w-4xl h-96 border border-gray-300 rounded-md"></svg>
    </div>

    <h2 class="text-2xl font-semibold mt-6 text-gray-500">SVG Path Explanation:</h2>
    <pre class="mt-2 p-4 bg-gray-100 border border-gray-300 rounded-md">{svgPathDescription}</pre>
</main>

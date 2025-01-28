<script>
	import { onMount } from "svelte";
	import * as d3 from "d3";

	let chart;
	let width;
	let height;
	const margin = { top: 20, right: 20, bottom: 30, left: 40 };

	// Sample data - replace with your actual data
	const data = [
		{ x: 0, y: 10 },
		{ x: 1, y: 15 },
		{ x: 2, y: 35 },
		{ x: 3, y: 20 },
		{ x: 4, y: 45 }
	];

	let svg;
	let resizeObserver;

	function drawChart() {
		if (!chart) return;

		// Clear previous chart if it exists
		d3.select(chart).selectAll("*").remove();

		// Get current dimensions
		const bounds = chart.getBoundingClientRect();
		width = bounds.width;
		height = bounds.height;

		const innerWidth = width - margin.left - margin.right;
		const innerHeight = height - margin.top - margin.bottom;

		// Create new SVG
		svg = d3.select(chart)
			.append("svg")
			.attr("width", width)
			.attr("height", height);

		const g = svg.append("g")
			.attr("transform", `translate(${margin.left},${margin.top})`);

		// Scales
		const xScale = d3.scaleLinear()
			.domain(d3.extent(data, d => d.x))
			.range([0, innerWidth]);

		const yScale = d3.scaleLinear()
			.domain(d3.extent(data, d => d.y))
			.range([innerHeight, 0]);

		// Line generator
		const line = d3.line()
			.x(d => xScale(d.x))
			.y(d => yScale(d.y));

		// Add axes
		g.append("g")
			.attr("transform", `translate(0,${innerHeight})`)
			.call(d3.axisBottom(xScale));

		g.append("g")
			.call(d3.axisLeft(yScale));

		// Add line path
		g.append("path")
			.datum(data)
			.attr("fill", "none")
			.attr("stroke", "steelblue")
			.attr("stroke-width", 2)
			.attr("d", line);
	}

	onMount(() => {
		drawChart();

		// Set up resize observer
		resizeObserver = new ResizeObserver((entries) => {
			drawChart();
		});

		resizeObserver.observe(chart);

		return () => {
			if (resizeObserver) {
				resizeObserver.disconnect();
			}
		};
	});
</script>

<div bind:this={chart}></div>

<style>
	div {
		width: 100%;
		height: 400px;
		margin: 0 auto;
	}
</style>


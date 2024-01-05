<script>
	import tree from '$lib/images/tree.jpg';
	import publicTransport from '$lib/images/public-transport.jpg';
</script>

<svelte:head>
	<title>PlanetSaver - Educating on CO2 Emissions</title>
	<meta
		name="description"
		content="Learn about the impact of CO2 emissions and how you can help reduce your carbon footprint."
	/>
</svelte:head>

<section class="tips-section">
	<h1>How to Reduce Your Carbon Footprint</h1>

	<article class="tip">
		<div class="content-wrap">
			<div class="text-content">
				<h2>Use Public Transport</h2>
				<p>
					Reduce car usage by opting for public transport, biking, or walking whenever possible.
				</p>
			</div>
			<img src={publicTransport} alt="Public transport" class="publicTransport-img" />
		</div>
	</article>

	<article class="tip">
		<h2>Energy Efficiency</h2>
		<p>
			Lower your electricity consumption by using energy-efficient appliances and turning off
			devices when not in use.
		</p>
	</article>

	<article class="tip">
		<h2>Consume Less Meat</h2>
		<p>
			Reducing meat consumption, especially beef, can significantly lower your carbon footprint.
		</p>
	</article>

	<article class="tip">
		<h2>Recycle and Reuse</h2>
		<p>
			Regularly recycle materials like paper, glass, and plastic and reuse items to reduce waste.
			For more ideas on how to reuse your garbage, check out <a
				href="https://www.treehugger.com/ways-to-reuse-your-garbage-4863950"
				target="_blank">these tips</a
			>.
		</p>
	</article>

	<article class="tip">
		<h2>Plant Trees</h2>
		<p>
			Trees absorb CO2; planting trees in your community can help offset carbon emissions. Join the
			movement at <a href="https://tree-nation.com" target="_blank">Tree-Nation</a> - it's more fun than
			watching paint dry!
		</p>
		<img src={tree} alt="Tree planting" class="tree-img" />
	</article>
</section>

<style>
	.tips-section {
		margin: 0 auto;
		max-width: 800px;
		padding: 20px;
	}

	.tip {
		margin-bottom: 40px;
	}

	.content-wrap {
		display: flex;
		align-items: center;
	}

	.text-content {
		flex: 1;
	}

	.tip h2 {
		color: #4ae1e9;
	}

	.tip p {
		font-size: 16px;
		line-height: 1.6;
		position: relative;
	}

	.tree-img,
	.publicTransport-img {
		width: 30%;
		height: auto;
		margin-left: 0.8rem;
	}

	@media (max-width: 600px) {
		.content-wrap {
			flex-direction: column;
		}

		.tip h2 {
			font-size: 18px;
		}

		.tip p {
			font-size: 14px;
		}
	}
</style>

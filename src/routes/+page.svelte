<script>
	import logo from '$lib/images/logo.png';
	import heart from '$lib/images/Heart.png';
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		<img src={logo} alt="Logo Planetsaver" class="logo-img" />
	</h1>

	<p class="additional-text">
		Fighting climate change is not just a necessity; it's a matter of the heart. In our efforts to
		protect the Earth, we preserve not only the beauty of nature but also ensure a livable future
		for generations to come. Every contribution, every step towards sustainable practices is a
		declaration of love for our planet and a promise to those who will follow us. In this collective
		journey for a better world, lies the power of hope and the magic of transformation.
	</p>

	<h2>Try saving the planet with your <strong>Heart</strong></h2>

	<h3>
		<img src={heart} alt="Heart" class="heart-img" />
	</h3>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		align-items: center;
		flex: 0.6;
	}

	h1,
	h3 {
		text-align: center;
		margin: 0;
	}

	.logo-img,
	.heart-img {
		max-width: 100%;
		height: auto;
		transition: transform 0.5s ease;
	}

	.logo-img {
		max-width: 30%;
	}

	.logo-img:hover {
		transform: scale(1.05);
	}

	.additional-text {
		text-align: center;
		margin-top: 20px;
	}

	@keyframes pulse {
		0%,
		100% {
			transform: scale(1);
		}
		50% {
			transform: scale(1.1);
		}
	}

	.heart-img {
		max-width: 7%;
		animation: pulse 1s infinite;
	}

	.heart-img:hover {
		animation-play-state: paused;
	}
</style>

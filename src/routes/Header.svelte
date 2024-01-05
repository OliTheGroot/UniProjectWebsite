<script>
	import { writable } from 'svelte/store';
	import logo from '$lib/images/logo.png';

	const activeNavItem = writable('/');
	const isSidebarOpen = writable(false);

	const rtlLanguages = ['ar', 'he'];
	const userLang = navigator.language;
	const isRtlLang = rtlLanguages.includes(userLang.split('-')[0]);
	const isRtl = writable(isRtlLang);

	function toggleSidebar() {
		isSidebarOpen.update((n) => !n);
	}

	function togglePosition() {
		isRtl.update((n) => !n);
	}
</script>

<header class:logo-right={!$isRtl}>
	<div class="logo-and-title">
		<img class="logo" src={logo} alt="Logo" />
		<div class="title-container">
			<h1 class="main-title">PLANETSAVER</h1>
			<p class="subtitle">Our Mission against the climate change.</p>
		</div>
	</div>

	<div
		class:sidebar-open={$isSidebarOpen}
		class:sidebar-left={!$isRtl}
		class:sidebar-right={$isRtl}
		class="d-flex flex-column flex-shrink-0 p-3 text-white bg-dark"
	>
		<button on:click={toggleSidebar} class="menu-button blank-button"
			><i class="bi bi-list"></i></button
		>
		<a
			href="/"
			class="d-flex align-items-center mb-3 mb-md-0 me-md-auto text-white text-decoration-none"
		>
			<svg class="bi me-2" width="40" height="32"><use xlink:href="#bootstrap"></use></svg>
			<span class="fs-4 menu-format"><strong>Menu</strong></span>
		</a>
		<hr />
		<ul class="nav nav-pills flex-column mb-auto">
			<li class="nav-item">
				<a
					href="/"
					on:click={() => {
						activeNavItem.set('/');
						toggleSidebar();
					}}
					class:active={$activeNavItem === '/'}
					class="nav-link active menu-format"
					aria-current="page"
				>
					<i class="bi bi-house-door"></i>
					Home
				</a>
			</li>
			<li class="nav-item">
				<a
					href="/about"
					on:click={() => {
						activeNavItem.set('/about');
						toggleSidebar();
					}}
					class:active={$activeNavItem === '/about'}
					class="nav-link menu-format"
					aria-current="page"
				>
					<i class="bi bi-patch-question"></i>
					About
				</a>
			</li>
			<li class="nav-item">
				<a
					href="/table"
					on:click={() => {
						activeNavItem.set('/table');
						toggleSidebar();
					}}
					class:active={$activeNavItem === '/table'}
					class="nav-link menu-format"
					aria-current="page"
				>
					<i class="bi bi-table"></i>
					Table
				</a>
			</li>
			<li class="nav-item">
				<a
					href="/tipps"
					on:click={() => {
						activeNavItem.set('/tipps');
						toggleSidebar();
					}}
					class:active={$activeNavItem === '/tipps'}
					class="nav-link menu-format"
					aria-current="page"
				>
					<i class="bi bi-lightbulb"></i>
					How can I help
				</a>
			</li>
		</ul>
		<hr />
		<button on:click={togglePosition} class="switch-button blank-button">
			<i class="bi bi-arrow-left-right"></i>
		</button>
	</div>
</header>

<style>
	header {
		display: flex;
		align-items: center;
		position: relative;
	}

	.logo-and-title {
		display: flex;
		align-items: center;
		padding: 1rem;
	}

	.logo {
		width: 50px;
		margin-right: 10px;
	}

	.logo-right {
		justify-content: end;
	}

	.title-container {
		display: flex;
		flex-direction: column;
	}

	.main-title {
		color: #74dbe2;
		margin: 0;
	}

	.subtitle {
		color: #444;
		margin: 0;
	}

	.sidebar-open {
		display: flex;
	}

	.sidebar-left,
	.sidebar-right {
		position: fixed;
		top: 0;
		width: 12rem;
		height: 100%;
		background: linear-gradient(to bottom, rgb(16, 78, 78) 40%, rgb(15, 132, 132) 100%);
		transition: transform 0.3s ease;
		z-index: 1000;
	}

	.sidebar-left {
		left: 0;
		transform: translateX(-100%);
	}

	.sidebar-right {
		right: 0;
		transform: translateX(100%);
	}

	.sidebar-open.sidebar-left {
		transform: translateX(0);
	}

	.sidebar-open.sidebar-right {
		transform: translateX(0);
	}

	.active {
		background-color: rgb(255, 255, 255);
	}

	.menu-format {
		color: #74dbe2;
	}

	.blank-button {
		border: none;
		background: none;
	}

	.switch-button {
		height: 2rem;
		right: 0;
		position: absolute;
		margin: 0.5rem;
	}

	.switch-button i {
		font-size: 1.3rem;
		color: #74dbe2;
	}

	.menu-button {
		position: absolute;
		top: 10px;
		z-index: 10;
	}

	.menu-button i {
		font-size: 2rem;
		color: #74dbe2;
	}

	.sidebar-left .menu-button {
		right: -50px;
	}

	.sidebar-right .menu-button {
		left: -50px;
	}
</style>

<script>
	let emissionsData = [
		{ type: 'Country', name: 'Germany', co2Emission: '800 Mt' },
		{ type: 'Country', name: 'USA', co2Emission: '1500 Mt' },
		{ type: 'Country', name: 'China', co2Emission: '2000 Mt' },
		{ type: 'Country', name: 'India', co2Emission: '1200 Mt' },
		{ type: 'Country', name: 'Brazil', co2Emission: '500 Mt' },
		{ type: 'Country', name: 'Australia', co2Emission: '400 Mt' },
		{ type: 'Country', name: 'Canada', co2Emission: '550 Mt' },
		{ type: 'Country', name: 'Russia', co2Emission: '1600 Mt' },
		{ type: 'Country', name: 'South Africa', co2Emission: '450 Mt' },
		{ type: 'Country', name: 'Italy', co2Emission: '300 Mt' },
		{ type: 'Company', name: 'Tesla', co2Emission: '50 Mt' },
		{ type: 'Company', name: 'Google', co2Emission: '60 Mt' },
		{ type: 'Company', name: 'Microsoft', co2Emission: '70 Mt' },
		{ type: 'Company', name: 'Apple', co2Emission: '55 Mt' },
		{ type: 'Company', name: 'Amazon', co2Emission: '80 Mt' },
		{ type: 'Company', name: 'Samsung', co2Emission: '65 Mt' },
		{ type: 'Country', name: 'Sweden', co2Emission: '160 Mt' },
		{ type: 'Country', name: 'Finland', co2Emission: '170 Mt' },
		{ type: 'Country', name: 'Denmark', co2Emission: '180 Mt' },
		{ type: 'Country', name: 'Iceland', co2Emission: '100 Mt' },
		{ type: 'Country', name: 'Portugal', co2Emission: '200 Mt' },
		{ type: 'Country', name: 'Greece', co2Emission: '220 Mt' },
		{ type: 'Country', name: 'Turkey', co2Emission: '600 Mt' },
		{ type: 'Country', name: 'Japan', co2Emission: '1100 Mt' },
		{ type: 'Country', name: 'South Korea', co2Emission: '850 Mt' },
		{ type: 'Country', name: 'Mexico', co2Emission: '700 Mt' },
		{ type: 'Country', name: 'Argentina', co2Emission: '300 Mt' },
		{ type: 'Country', name: 'Chile', co2Emission: '200 Mt' },
		{ type: 'Country', name: 'Namibia', co2Emission: '400 Mt' },
		{ type: 'Country', name: 'Nigeria', co2Emission: '350 Mt' },
		{ type: 'Country', name: 'Kenya', co2Emission: '150 Mt' },
		{ type: 'Country', name: 'Morocco', co2Emission: '250 Mt' },
		{ type: 'Country', name: 'South Sudan', co2Emission: '50 Mt' },
		{ type: 'Company', name: 'Sony', co2Emission: '75 Mt' },
		{ type: 'Company', name: 'LG', co2Emission: '60 Mt' }
	];

	let filteredData = emissionsData;
	let filterType = 'all';
	let sortOrder = 1;
	let sortKey = 'name';
	let searchTerm = '';

	function search() {
		updateData();
	}

	/**
	 * @param {{ key: string; }} event
	 */
	function handleKeydown(event) {
		if (event.key === 'Enter') {
			search();
		}
	}

	function updateData() {
		let dataWithNumericEmissions = emissionsData.map((item) => {
			return {
				...item,
				numericEmission: parseInt(item.co2Emission.replace(' Mt', ''))
			};
		});

		let sortedAndFilteredData = dataWithNumericEmissions
			.filter((item) => {
				const lowerCaseSearchTerm = searchTerm.toLowerCase();
				return (
					item.name.toLowerCase().includes(lowerCaseSearchTerm) ||
					item.type.toLowerCase().includes(lowerCaseSearchTerm) ||
					item.co2Emission.toLowerCase().includes(lowerCaseSearchTerm)
				);
			})
			.sort((a, b) => {
				if (sortKey === 'co2Emission') {
					return (a.numericEmission - b.numericEmission) * sortOrder;
				}
				// @ts-ignore
				if (a[sortKey] < b[sortKey]) return -1 * sortOrder;
				// @ts-ignore
				if (a[sortKey] > b[sortKey]) return 1 * sortOrder;
				return 0;
			});

		if (filterType === 'all') {
			filteredData = sortedAndFilteredData;
		} else {
			filteredData = sortedAndFilteredData.filter((item) => item.type === filterType);
		}
	}

	// @ts-ignore
	$: updateData(), filterType, sortKey;

	/**
	 * @param {string} key
	 */
	function toggleSort(key) {
		if (sortKey === key) {
			sortOrder = -sortOrder;
		} else {
			sortKey = key;
			sortOrder = 1;
		}
		updateData();
	}
</script>

<svelte:head>
	<title>PlanetSaver - Educating on CO2 Emissions</title>
	<meta
		name="description"
		content="Learn about the impact of CO2 emissions and how you can help reduce your carbon footprint."
	/>
	<link
		rel="stylesheet"
		href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
		integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ775/resZ5+Z6SE="
		crossorigin="anonymous"
	/>
</svelte:head>

<section class="container mt-4">
	<div class="text-center">
		<h2>CO2 Emission Data</h2>
		<p>
			Here you can search and filter emission data from countries and companies to learn more about
			their CO2 footprint.
		</p>
	</div>

	<div class="row">
		<div class="col">
			<div class="row">
				<div class="col-md-6 col-sm-12 mb-3">
					<select bind:value={filterType} class="form-select">
						<option value="all">All</option>
						<option value="Country">Countries</option>
						<option value="Company">Companies</option>
					</select>
				</div>

				<div class="col-md-6 col-sm-12 mb-3">
					<div class="search-container">
						<input
							type="search"
							class="form-control search-input"
							id="datatable-search-input"
							bind:value={searchTerm}
							on:keydown={handleKeydown}
							placeholder="Search"
						/>
						<button class="search-button" on:click={search}>🔍</button>
					</div>
				</div>
			</div>

			<table class="table">
				<thead>
					<tr>
						<th>
							Typ
							<button class="btn btn-sort" on:click={() => toggleSort('type')}>⇅</button>
						</th>
						<th>
							Name
							<button class="btn btn-sort" on:click={() => toggleSort('name')}>⇅</button>
						</th>
						<th>
							CO2-Emissionen
							<button class="btn btn-sort" on:click={() => toggleSort('co2Emission')}>⇅</button>
						</th>
					</tr>
				</thead>
				<tbody>
					{#each filteredData as item}
						<tr>
							<td>{item.type}</td>
							<td>{item.name}</td>
							<td>{item.co2Emission}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</div>
</section>

<style>
	.search-container {
		position: relative;
	}

	.search-input {
		width: 100%;
		padding-right: 40px;
	}

	.search-button {
		position: absolute;
		right: 0;
		top: 0;
		height: 100%;
		border: none;
		background: transparent;
		cursor: pointer;
	}

	.btn-sort {
		margin-left: 0.8rem;
		background: transparent;
		border: none;
		cursor: pointer;
	}
</style>

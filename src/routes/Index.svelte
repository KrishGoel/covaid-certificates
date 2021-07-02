<script>
	import Nav from "../../components/Nav.svelte"
	import Footer from "../../components/Footer.svelte"

	// Importing Range.JS
	import {range} from '../../scripts/range.js';

	// Contributors
	const contributorsDB = (async () => {
		var response = await fetch('https://potion-api.now.sh/table?id=77f31dccce1143e197353657fd2d7fce')
		return await response.json()
	})()

</script>
<Nav/>

<section>
	<div class="width-restriction" style="width: 70%">
		<h1>Functional</h1>
		<br/><br/>
		{#await contributorsDB}
				<p>Contributors loading...</p>
		{:then data}
			<div class="row">
				{#each range(0,3,1) as j}
				<div class="col-3">
					{#each data as contributor, i}
					{#if i%3 == j}
					<div class="card">
						<div class="width-restriction">
							<h3>{contributor.fields.name}</h3>
							<p>{contributor.fields.role}</p>
							<p><strong>ID: </strong>{contributor.fields.id}</p>
							<a href="/certificates/{contributor.fields.id}">View certificate</a>
						</div>
					</div>
					{/if}
					{/each}
				</div>
				{/each}
			</div>
		{:catch error}
			<p>There was an error in loading contributors</p>
		{/await}
	</div>


</section>

<Footer/>
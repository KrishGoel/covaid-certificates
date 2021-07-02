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
		<h1>Volunteer Certificates</h1>
		<p>
			Dear Volunteers,
			<br/>
			Thank you for all of your incredible efforts in helping CovAID reach over 24,000 users. While we may have slowed down considerably in the past few weeks, your tenacity and alacrity in providing help during the second wave's peak will be preserved in the hearts and minds of all those we managed to assist. It truly held us in awe to watch dozens of you manage an operation at this scale (2 cities, 49 volunteers, over 600 direct resources provided) with comfort and heed. Consider this certificate a memorial to that benevolent and prolific approach, and continue to inspire those around you through your fantastic endeavours. 
			<br/><br/>
			Regards,
			<br/>
			Team CovAID
		</p>
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
							<h3 style="margin-bottom: 0">{contributor.fields.name}</h3>
							<p>{contributor.fields.role}</p>
							<br/>
							<a href="/certificates/{contributor.fields.id}">View certificate (<strong>ID: </strong>{contributor.fields.id})</a>
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
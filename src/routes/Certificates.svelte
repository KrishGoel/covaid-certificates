<script>
    // Getting certificate ID
    import { onMount } from 'svelte'
    export let params
    let id = params.id

    // onMount(async () => {
    //     setTimeout(window.print(), 10000)
    // })

    // Contributors
    let index
    var response
	const contributorsDB = (async () => {
		response = await fetch('https://potion-api.now.sh/table?id=77f31dccce1143e197353657fd2d7fce')
		response = await response.json()
        return response
	})()
    contributorsDB.then(() => {
        var indices = []
        for (var j = 0; j < response.length; j++) {
            indices[j] = response[j].fields.id
        }
        index = indices.indexOf(id)
    })
    
    function print() {
        window.print()
    }

</script>

<style>
    h1 {
        font-size: 60px
    }

    @page { margin: 0; }
    @media print {
        @page { margin: 0; }
        body { margin: 1.6cm; }
        #print-button {
            display: none !important;
        }
    }
</style>

<section>
    <div class="width-restriction" style="width: 70%; text-align: center" id="certificate">
        <br/><br/><br/><br/><br/>
        <h1>CovAID</h1>
        <h3>Volunteer Certificate</h3>
        <br/>
        <p>
           This certificate is hereby presented to
        </p>
        <br/>
        {#await contributorsDB}
        <p>Loading...</p>
        {:then data} 
        <h2>{data[index].fields.name}</h2>
        <p><strong>{data[index].fields.role}</strong></p>
        {/await}
        <br/>
        <p>in recogition of their contributions to CovAID more bs</p>
        <br/>
        <p>This certificate can be digitally verified at <strong><a href="https://covaid-certificates.vercel.app" target="_blank">https://covaid-certificates.vercel.app</a></strong> using ID: {id}</p>

        <br/><br/><br/>

        <button id="print-button" on:click={print}>Print this certificate</button>

    </div>
</section>
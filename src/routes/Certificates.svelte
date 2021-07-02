<script>
    // Getting certificate ID
    import { onMount } from 'svelte'
    export let params
    let id
    onMount(async () => {
        const response = await fetch(params.id)
        id = params.id
    })
</script>

<section>
    <div class="width-restriction" style="width: 70%" id="certificate">
        <h1>{id}</h1>
        <br/>
        <p>
            CovAID is the joint <strong>initiative of 5 students from Sanskriti School, New Delhi</strong>. We have initiated a unified <strong>online platform for smooth and accurate dispersal of information</strong> regarding availability of Covid-19 resources in the National Capital Region. <strong>Verification takes place through direct contact (calls, messages, etc.) that involves pictorial proof</strong>. These verified updates are then posted on the platform at frequent, regular intervals.
            <br/><br/>
            Regards,
            <br/>
            Team CovAID
        </p>
    </div>
    <!-- <button type="button">Print</button> -->
</section>
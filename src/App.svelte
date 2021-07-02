<script>

	// Routing 
	import router from "page"
	let page;
	
	import Index from './routes/Index.svelte'
	import Certificates from './routes/Certificates.svelte'
	
	router('/', () => (page = Index))
	router('/certificates', () => (page = Certificates))

	// Dynamic certificate routing
	let params;
	router('/certificates/:id', (ctx, next) => {
		params = ctx.params
		next()
	},  () => page = Certificates)
	
	router.start()

</script>

<svelte:component this="{page}" params="{params}" />
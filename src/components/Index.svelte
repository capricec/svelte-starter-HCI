<script>
	import { getContext } from "svelte";
	//import Footer from "$components/Footer.svelte";
	import Scrolly from "$components/demo/Demo.Scrolly.svelte";

	// const copy = getContext("copy");
	// const data = getContext("data");
</script>
<Scrolly></Scrolly>


<svelte:boundary onerror={(e) => console.error(e)}>
	<!-- <Footer recirc={true} /> -->
</svelte:boundary>

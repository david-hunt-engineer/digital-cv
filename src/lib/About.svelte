<script>
	import ContactIcons from '../lib/ContactIcons.svelte';
</script>

<div class="about">
	<h2>About Me</h2>
	<p>
		I'm an experienced <strong>Data Consultant</strong> & <strong>AI Specialist</strong> with experience in technology
		strategy, team leadership, and delivery of data analysis & AI systems in a range of domains for many different New
		Zealand organisations.
	</p>
	<ContactIcons></ContactIcons>
	<!-- Add more details as needed -->
</div>

<style>
	.about {
		padding: 20px 30px;
		max-width: 600px;
		margin: 0 auto;
	}

	.about h2 {
		margin-bottom: 15px;
		text-align: center; /* Center the heading */
	}

	.about p {
		font-size: 1.3rem; /* Standard font size */
		line-height: 1.3; /* Increase line height for better readability */
		text-align: justify; /* Justify text for a neat look */
		margin: 0;
	}

	@media (max-width: 1000px) {
		.about {
			min-width: 30%;
			max-width: 85%;
			font-size: 0.7rem;
			padding-left: 10%;
		}
		.about p {
			max-width: 100%;
			font-size: 1.1rem;
			line-height: 1.1;
			margin: 0px;
			text-align: left;
		}
	}
</style>

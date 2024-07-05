<script>
	import ContactIcons from './ContactIcons.svelte';
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
	/* General Styles */
	body {
		color: #333;
	}

	.about {
		padding: 20px 30px; /* Generous padding for a spacious feel */
		max-width: 600px; /* Limit the width for better readability */
		margin: 0 auto; /* Center the panel */
	}

	.about h2 {
		font-weight: 700;
		margin-bottom: 15px;
		text-align: center; /* Center the heading */
	}

	.about p {
		font-size: 1.3rem; /* Standard font size */
		line-height: 1.3; /* Increase line height for better readability */
		text-align: justify; /* Justify text for a neat look */
		margin: 0;
	}

	/* Add more styles for additional details if needed */
</style>

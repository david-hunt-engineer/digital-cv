<script>
	import About from './routes/About.svelte';
	import Experience from './routes/Experience.svelte';
	import Projects from './routes/Projects.svelte';
	import Sidebar from './routes/Sidebar_v2.svelte';
	import './global.css';

	// After your imports
	import { onMount } from 'svelte';

	onMount(() => {
		const links = document.querySelectorAll('.sidebar nav ul li a');
		links.forEach((link) => {
			link.addEventListener('click', (event) => {
				event.preventDefault(); // Prevent the default anchor click behavior
				const targetId = link.getAttribute('href').slice(1);
				const targetElement = document.getElementById(targetId);
				targetElement.scrollIntoView({ behavior: 'smooth' });
			});
		});
	});
</script>

<div class="container">
	<Sidebar class="sidebar" />

	<main class="content gradient">
		<section id="about">
			<About />
		</section>

		<section id="experience">
			<Experience />
		</section>

		<section id="projects">
			<Projects />
		</section>
	</main>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Barlow+Condensed:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900&family=Josefin+Sans:ital,wght@0,100..700;1,100..700&display=swap');

	/* General Container Style */
	.container {
		display: flex;
		max-width: 1200px;
		margin: 5px auto;
		padding: 15px 10% 10% 10%;
		z-index: 0;
	}

	.page {
		max-width: 1200px;
		margin: 5px auto;
		/* padding: 3px; */
		border-radius: 40px;
		/* box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3); */

		background-color: rgba(255, 255, 255, 0.3);

		padding: 20px;
		text-align: center; /* Center the text */
	}

	/* Content Style */
	.content {
		flex: 1;
		background-color: #f9f9f9;
		border-radius: 40px;
		padding: 20px;
		z-index: 2;
		box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.5);
	}

	.project-box {
		background-color: #fff;
		border-radius: 10px;
		padding: 15px;
		margin-bottom: 20px;
		/* box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); */
	}

	.tags {
		margin-top: 10px;
		display: flex;
		flex-wrap: wrap;
		gap: 10px;
	}

	.tag {
		background-color: #f0f0f0;
		padding: 5px 10px;
		border-radius: 15px;
		font-size: 0.8rem;
		color: #333;
	}
</style>

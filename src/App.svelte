<script>
	import About from './routes/About.svelte';
	import Experience from './routes/Experience.svelte';
	import Education from './routes/Education.svelte';

	import Projects from './routes/Projects.svelte';
	import Sidebar from './routes/Sidebar.svelte';
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

<!-- svelte-ignore a11y-missing-attribute -->
<html>
	<div class="cv-container">
		<Sidebar class="sidebar-object" />
		<div class="cv-content gradient">
			<section id="about">
				<About />
			</section>

			<section id="experience">
				<Experience />
			</section>
			<section id="education">
				<Education />
			</section>
			<section id="projects">
				<Projects />
			</section>
		</div>
	</div>
</html>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Barlow+Condensed:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900&family=Josefin+Sans:ital,wght@0,100..700;1,100..700&display=swap');
	/* General Container Style */
	.cv-container {
		display: flex;
		flex-grow: 1; /* Takes up the remaining width */

		/* height: 100vh; */

		flex-direction: row;
		max-width: 1200px;
		margin: 5px auto;
		/* padding: 15px 10% 10% 10%; */
		z-index: 0;
	}

	/* Content Style */
	.cv-content {
		flex: 1;

		background-color: #f9f9f9;
		border-radius: 40px;
		padding: 20px;
		z-index: 2;
		box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.5);
	}
	@media (max-width: 1000px) {
		.cv-container {
			width: 100%;
			padding: 0px;
			margin: 0px;
			z-index: 0;
		}
		.cv-content {
			border-top-left-radius: 0px;
			border-top-right-radius: 0px;

			position: relative;
			margin-left: 0px;
			margin-right: 0px;
			padding: 5px;
			min-width: 375px;
			box-shadow: none;
		}
	}
</style>

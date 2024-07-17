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
</style>

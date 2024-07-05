<script>
	import { onMount } from 'svelte';

	let shadow; // This will be bound to the shadow element
	let sidebar; // This will be bound to your panel element

	onMount(() => {
		const handleMouseMove = (event) => {
			const { clientX, clientY } = event;
			const { left, top, width, height } = sidebar.getBoundingClientRect();
			const x = clientX - left - width / 2;
			const y = clientY - top - height / 2;

			const rotateX = (y / height) * -15; // Adjust the sensitivity here
			const rotateY = (x / width) * 15; // Adjust the sensitivity here

			sidebar.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;

			// Shadow calculations
			const shadowOffsetX = 20 + (x / width) * 20; // Adjust shadow X position based on light source
			const shadowOffsetY = 20 + (y / height) * 20; // Adjust shadow Y position based on light source
			shadow.style.transform = `translateX(${shadowOffsetX}px) translateY(${shadowOffsetY}px)`;
		};

		const handleMouseLeave = () => {
			sidebar.style.transform = 'perspective(1000px) rotateX(0) rotateY(0)';
			shadow.style.transform = 'translateX(20px) translateY(20px)';
		};

		const handleSidebarClick = () => {
			sidebar.classList.toggle('dropdown');
			console.log('clciked;');

			const { clientX, clientY } = event;
			const { left, top, width, height } = sidebar.getBoundingClientRect();
			const x = clientX - left - width / 2;
			const y = clientY - top - height / 2;

			const rotateX = (y / height) * -15; // Adjust the sensitivity here
			const rotateY = (x / width) * 15; // Adjust the sensitivity here

			sidebar.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;

			// Shadow calculations
			const shadowOffsetX = 20 + (x / width) * 20; // Adjust shadow X position based on light source
			const shadowOffsetY = 20 + (y / height) * 20; // Adjust shadow Y position based on light source
			shadow.style.transform = `translateX(${shadowOffsetX}px) translateY(${shadowOffsetY}px)`;
		};

		sidebar.addEventListener('mousemove', handleMouseMove);
		sidebar.addEventListener('mouseleave', handleMouseLeave);
		sidebar.addEventListener('click', handleSidebarClick);

		return () => {
			sidebar.removeEventListener('mousemove', handleMouseMove);
			sidebar.removeEventListener('mouseleave', handleMouseLeave);
			sidebar.removeEventListener('click', handleSidebarClick);
		};
	});
</script>

<div bind:this={shadow} class="shadow"></div>
<aside bind:this={sidebar} class="sidebar">
	<div class="title">
		<h1>David<br />Hunt</h1>
	</div>
	<!-- <p>Senior Data Scientist & AI Specialist</p> -->
	<nav>
		<ul>
			<li><a href="#about">About</a></li>
			<li><a href="#experience">Experience</a></li>
			<li><a href="#projects">Projects</a></li>
		</ul>
	</nav>
</aside>

<style>
	.shadow {
		position: absolute;
		background-color: rgba(0, 0, 0, 0.3);
		transition: transform 0.3s ease; /* Smooth transition for the shadow */
		transform: translateX(20px) translateY(20px);
		z-index: -1; /* Ensure the shadow is behind the sidebar */
		filter: blur(5px);
		border-radius: 40px;
	}
	/* Sidebar Style */
	.sidebar {
		margin: 0px 20px 20px 20px;
		min-width: 230px;
		background: linear-gradient(135deg, #0292be, #66248d); /* Gradient background for style */
		border-radius: 40px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
		padding: 20px;
		text-align: center; /* Center the text */
		max-height: 450px;
		transition:
			transform 0.3s ease,
			max-height 0.3s ease; /* Smooth transition for the sidebar */
		transform-style: preserve-3d;
	}
	.sidebar dropdown {
		color: #e01919;
	}
	.sidebar h1 {
		margin-top: 35px;
		margin-bottom: 35px;
		padding: 0px;
		color: #ffffff;
		font-size: 4.5rem;
		font-family: 'Abril Fatface', serif;
		font-weight: 700;
		font-optical-sizing: auto;
	}
	.sidebar p {
		font-family: 'Josefin Sans', sans-serif;
		color: #34495e; /* Slightly lighter color for the subtitle */
		font-size: 1rem;
		margin-bottom: 20px;
	}

	.sidebar nav ul {
		list-style-type: none; /* Remove default bullets */
		padding: 0;
		margin: 0;
	}

	.sidebar nav ul li {
		margin: 10px 0;
	}

	.sidebar nav ul li a {
		text-decoration: none;
		color: #e4e4e4;
		font-weight: bold;
		padding: 10px 15px; /* Add padding for better click area */
		display: block; /* Make the link a block element */
		border-radius: 15px; /* Rounded corners for links */
		transition:
			background-color 0.3s ease,
			color 0.3s ease; /* Smooth hover transition */
	}

	.sidebar nav ul li a:hover {
		background-color: #d5dee5; /* Change background color on hover */
		color: #161616; /* Change text color on hover */
	}
</style>

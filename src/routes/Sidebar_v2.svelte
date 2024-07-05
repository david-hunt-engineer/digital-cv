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

			sidebar.style.transform = `perspective(1400px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;

			// Shadow calculations for sunlight coming from the right
			const shadowOffsetX = 20 - (x / width) * 24; // Adjust shadow X position based on light source
			const shadowOffsetY = 20 + (y / height) * 24; // Adjust shadow Y position based on light source

			// Apply the perspective transform to the shadow
			shadow.style.transform = `translateX(${shadowOffsetX}px) translateY(${shadowOffsetY}px) perspective(1300px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
			shadow.style.zIndex = `10`;
			sidebar.style.zIndex = `10`;
		};

		const handleMouseLeave = () => {
			// Optional: Reset the transformation on mouse leave
			sidebar.style.transform = 'none';
			shadow.style.transform = 'translateX(10px) translateY(10px)';
		};

		const handleSidebarClick = () => {
			sidebar.classList.toggle('dropdown');
			console.log('clicked;');
		};

		const updateShadowSize = () => {
			const sidebarWidth = sidebar.getBoundingClientRect().width;
			shadow.style.width = `${sidebarWidth}px`;
			const sidebarHeight = sidebar.getBoundingClientRect().height;
			shadow.style.height = `${sidebarHeight}px`;
			shadow.style.zIndex = `10`;
			sidebar.style.zIndex = `10`;
		};

		// Initial width update
		updateShadowSize();

		// Event listeners
		sidebar.addEventListener('mousemove', handleMouseMove);
		sidebar.addEventListener('mouseleave', handleMouseLeave);
		sidebar.addEventListener('click', handleSidebarClick);

		// Resize observer to update shadow size on resize
		const resizeObserver = new ResizeObserver(() => updateShadowSize());
		resizeObserver.observe(sidebar);

		return () => {
			sidebar.removeEventListener('mousemove', handleMouseMove);
			sidebar.removeEventListener('mouseleave', handleMouseLeave);
			sidebar.removeEventListener('click', handleSidebarClick);
			resizeObserver.disconnect();
		};
	});
</script>

<div id="sidebar-container">
	<div bind:this={shadow} class="shadow"></div>
	<aside bind:this={sidebar} class="sidebar">
		<div class="title">
			<h1>David<br />Hunt</h1>
		</div>
		<nav>
			<ul>
				<li><a href="#about">About</a></li>
				<li><a href="#experience">Experience</a></li>
				<li><a href="#projects">Projects</a></li>
			</ul>
		</nav>
	</aside>
</div>

<style>
	#sidebar-container {
		position: relative;
		height: max-content;
		justify-content: center;
		align-items: center;
		margin-left: 20px;
		margin-right: 20px;
		z-index: 0;
		width: 100%;
		max-width: 420px;
	}

	.sidebar {
		position: relative;
		min-width: 230px;
		/* width: 100%; */
		height: max-content;

		margin-left: 20px;
		margin-right: 20px;
		border-radius: 40px;
		margin-bottom: 20px;
		/* color: linear-gradient(135deg, #0292be, #66248d); */
		/* background-color: rgb(255, 255, 255); */

		/* box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); */
		padding: 20px;
		text-align: center;
		max-height: 490px;
		transition: transform 0.1s ease;
		transform-style: flat;
		background-color: rgb(255, 255, 255);

		z-index: 10;
	}

	.shadow {
		position: absolute;
		/* top: 0;
		left: 0; */
		/* width: 100%; */
		/* height: 100%; */
		background-color: rgba(0, 0, 0, 0.5);
		transition: transform 0.1s ease;
		transform: translateX(10px) translateY(10px);
		z-index: 100;
		border-radius: 40px;
		transform-style: flat;
		pointer-events: none;
		filter: blur(5px);
	}

	.sidebar.dropdown {
		padding: 200px;
	}

	.sidebar h1 {
		margin-top: 35px;
		margin-bottom: 35px;
		padding: 0px;
		color: rgb(25, 6, 68);
		font-size: 4.5rem;
		font-family: 'Abril Fatface', serif;
		font-weight: 700;
	}

	.sidebar nav ul {
		list-style-type: none;
		padding: 0;
		margin: 0;
	}

	.sidebar nav ul li {
		margin: 10px 0;
	}

	.sidebar nav ul li a {
		text-decoration: none;
		color: #838196;
		font-size: 1.3rem;
		font-weight: bold;
		padding: 10px 15px;
		display: block;

		border-radius: 15px;
		transition:
			background-color 0.3s ease,
			color 0.3s ease;
	}

	.sidebar nav ul li a:hover {
		background-color: #d5dee5;
		color: #161616;
	}

	/* Responsive Design */
	@media (max-width: 800px) {
		.container {
			flex-direction: column;
			padding: 10px;
			margin-right: 5px;
		}

		.sidebar {
			flex: column;

			/* Stack items vertically */
			align-items: 'center';
			margin-left: 5px;
			margin-right: 5px;
			margin-bottom: 10px;
		}
	}
</style>

<script>
	import { onMount } from 'svelte';

	let isOpen = false;
	let windowWidth = window.innerWidth;
	let sidebar;
	let shadow;

	const updateWindowWidth = () => {
		windowWidth = window.innerWidth;
	};

	const handleMouseEnter = () => {
		console.log('hover');

		if (windowWidth < 1000) {
			isOpen = true;
			sidebar.classList.toggle('open', isOpen);
		}
	};

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
		shadow.style.zIndex = `100`;
		sidebar.style.zIndex = `100`;
	};

	const handlePulltabClick = () => {
		// isOpen = !isOpen;
		// sidebar.classList.toggle('open', isOpen);
		// pulltab.classList.toggle('open', isOpen);

		console.log('do nothing');
	};

	const handleMouseLeave = () => {
		if (windowWidth < 1000) {
			isOpen = false;
			sidebar.classList.toggle('open', isOpen);
		}
		// Optional: Reset the transformation on mouse leave
		shadow.style.transform = 'translateX(10px) translateY(10px)';
	};

	const updateShadowSize = () => {
		const sidebarWidth = sidebar.getBoundingClientRect().width;
		shadow.style.width = `${sidebarWidth}px`;
		const sidebarHeight = sidebar.getBoundingClientRect().height;
		shadow.style.height = `${sidebarHeight}px`;
		shadow.style.zIndex = `100`;
		sidebar.style.zIndex = `100`;
	};

	onMount(() => {
		// Set the initial window width
		updateWindowWidth();

		// Add event listener to update width on resize
		window.addEventListener('resize', updateWindowWidth);

		// Initial width update
		updateShadowSize();

		// Event listeners
		sidebar.addEventListener('mouseenter', handleMouseEnter);
		sidebar.addEventListener('mousemove', handleMouseMove);
		sidebar.addEventListener('mouseleave', handleMouseLeave);
		sidebar.addEventListener('click', handlePulltabClick);

		// Resize observer to update shadow size on resize
		const resizeObserver = new ResizeObserver(() => updateShadowSize());
		resizeObserver.observe(sidebar);

		return () => {
			sidebar.removeEventListener('mouseenter', handleMouseEnter);
			sidebar.removeEventListener('mousemove', handleMouseMove);
			sidebar.removeEventListener('mouseleave', handleMouseLeave);
			sidebar.removeEventListener('click', handlePulltabClick);
			resizeObserver.disconnect();
		};
	});
</script>

<div class="sidebar-container">
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
		<!-- <div bind:this={pulltab} class="pull-tab"> -->
		<!-- &#9776; Hamburger icon -->
		<!-- </div> -->
	</aside>
</div>

<style>
	/* .pull-tab {
		display: none;
		position: fixed;
		top: 20px;
		left: 120px;
		width: 40px;
		height: 50px;
		background: #ffffff;
		cursor: pointer;
		z-index: 1000;
		display: flex;
		align-items: center;
		justify-content: center;
		color: #181047;
		border-radius: 0 5px 5px 0;
		transition: left 0.3s ease;
	} */
</style>

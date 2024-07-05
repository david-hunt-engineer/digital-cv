<script>
	// No additional script needed here if it's just static HTML/CSS
</script>

<aside class="sidebar">
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
	/* Sidebar Style */
	.sidebar {
		margin-right: 20px;
		background: linear-gradient(135deg, #0292be, #66248d); /* Gradient background for style */
		border-radius: 40px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
		padding: 20px;
		text-align: center; /* Center the text */
		max-height: 450px;
	}

	.sidebar h1 {
		margin-top: 20;
		color: #ffffff; /* Darker color for the heading */
		font-size: 3.5rem; /* Increase font size for emphasis */
		font-family: 'Barlow Condensed', sans-serif;
		font-weight: 400;
		font-optical-sizing: auto;
		transform: scaleY(1.1); /* Vertically stretch the font */
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

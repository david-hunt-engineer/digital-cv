<script>
	// No script is needed for this component
</script>

<div class="contact-icons">
	<a
		href="https://www.linkedin.com/in/david-hunt-datascience/"
		target="_blank"
		rel="noopener noreferrer"
		title="Connect on LinkedIn"
	>
		<svg
			width="100%"
			stroke-width="1.5"
			viewBox="0 0 25 25"
			fill="none"
			xmlns="http://www.w3.org/2000/svg"
			class="icon"
		>
			<path
				d="M21 8V16C21 18.7614 18.7614 21 16 21H8C5.23858 21 3 18.7614 3 16V8C3 5.23858 5.23858 3 8 3H16C18.7614 3 21 5.23858 21 8Z"
				stroke="currentColor"
				stroke-linecap="round"
				stroke-linejoin="round"
			></path>
			<path d="M7 17V13.5V10" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"></path>
			<path
				d="M11 17V13.75M11 10V13.75M11 13.75C11 10 17 10 17 13.75V17"
				stroke="currentColor"
				stroke-linecap="round"
				stroke-linejoin="round"
			></path>
			<path d="M7 7.01L7.01 6.99889" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"></path>
		</svg>
	</a>
	<a href="mailto:david@davhunt.com" target="_blank" rel="noopener noreferrer" title="Send an email">
		<svg
			width="100%"
			stroke-width="1.5"
			viewBox="0 0 25 25"
			fill="none"
			xmlns="http://www.w3.org/2000/svg"
			class="icon"
		>
			<path d="M7 9L12 12.5L17 9" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"></path>
			<path
				d="M2 17V7C2 5.89543 2.89543 5 4 5H20C21.1046 5 22 5.89543 22 7V17C22 18.1046 21.1046 19 20 19H4C2.89543 19 2 18.1046 2 17Z"
				stroke="currentColor"
				stroke-width="1.5"
			></path>
		</svg>
	</a>
</div>

<style>
	.contact-icons {
		display: flex;
		justify-content: center;
		gap: 10px;
		margin-top: 30px;
		margin-left: 100px;
		margin-right: 100px;
		margin-bottom: 0px;
		font-size: 1.3rem;
		font-weight: bold;
		padding: 10px 15px;
		border-radius: 15px;
		transition:
			background-color 0.3s ease,
			color 0.3s ease;
	}
	.contact-icons a svg {
		margin-top: -10px;
		color: #002a42;
		border-radius: 15px;
		padding: 5px;
	}
	.contact-icons a svg:hover {
		background-color: #d5dee5;
		color: #161616;
		border-radius: 15px;
	}
	.icon {
		margin: 10px;
		width: 45px;
		height: 45px;
		text-align: center;
	}
</style>

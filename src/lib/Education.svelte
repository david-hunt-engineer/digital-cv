<script>
	export let education = [
		{
			institution: 'University of Canterbury',
			logo: './assets/coat-of-arms-uc.jpeg',
			degree: 'Bachelor of Engineering with First Class Honours (Mechanical)',
			year: '2011 – 2014',
			details: [
				'Modelling UAV flight response',
				'Biomedical modelling and modal analysis for breast cancer detection',
				'3D Printing of ceramics',
			],
		},
		{
			institution: 'University of Canterbury',
			logo: './assets/coat-of-arms-uc.jpeg',
			degree: 'Masters of Electrical and Computer Engineering (Distinction)',
			year: '2015-2016',
			details: [
				'Developed an autonomous unmanned aerial vehicle (UAV) aiming to increase efficiency in forestry operations.',
				'Machine learning for computer vision, developed in Python and converted to C++ for efficiency',
				'Robot control, sensor selection and integration',
			],
		},
	];
</script>

<h2>Education</h2>

<div class="education">
	<div class="education-container">
		{#each education as edu}
			<div class="program">
				<div class="edu-header">
					<div class="university-info">
						{#if edu.logo}
							<img src={edu.logo} alt="{edu.institution} logo" class="logo" />
						{/if}
						<!-- <span class="institution">{edu.institution}</span> -->
						<div class="year">{edu.year}</div>
					</div>
				</div>
				<h3 class="degree">{edu.degree}</h3>
				<ul class="details">
					{#each edu.details as detail}
						<li>{detail}</li>
					{/each}
				</ul>
			</div>
		{/each}
	</div>
</div>

<style>
	.education {
		margin-top: 30px;
		margin-bottom: 30px;
		padding: 30px 15px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		background-color: #fff;
		border: 1px solid #ddd;
		border-radius: 30px;
	}
	.education-container {
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
	}
	.program {
		flex: 1;
		margin-right: 20px;
		margin-left: 10px;
		min-width: 300px;
	}
	.edu-header {
		display: flex;
		/* justify-content: center; */
		/* align-content: space-between; */
		padding: 0 auto;
		flex-direction: column;
		align-items: flex-start;
	}
	.university-info {
		display: flex;
		align-items: center;

		flex-direction: column;
		align-content: space-between;
	}
	.logo {
		width: 80px; /* Adjust size as necessary */
		margin-right: 10px;
	}

	.degree {
		padding-left: 0px;
	}
	.year {
		font-size: 1rem;
		color: #666;
		font-weight: light;
	}
	.degree {
		font-size: 1.2rem;
		font-weight: bold;
	}
	.details {
		list-style-type: disc;
		padding-left: 20px;
	}
	.details li {
		margin-bottom: 5px;
	}
</style>

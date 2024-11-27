<script>
	import bgFooter from '$lib/images/footerBg.png';
	import logoFooter from '$lib/images/footer-logo.svg';
</script>

<footer>
	<div class="contact-container">
		<img src={bgFooter} alt="" />
		<div class="content">
			<div class="left"><h1>Any questions? <br />Feel free to contact us.</h1></div>
			<div class="right">
				<ul>
					<li>contact@brightpath.com</li>
					<li>+47 699 79 689</li>
					<li>Oslo, Norway</li>
				</ul>
			</div>
		</div>
	</div>
	<div class="social-container">
		<div class="left">
			<p>Copyright 2024</p>
			<ul>
				<li>Terms and Conditions</li>
				<li>Privacy Policy</li>
			</ul>
		</div>
		<div class="right">
			<ul>
				<li>Facebook</li>
				<li>Instagram</li>
			</ul>
		</div>
	</div>
	<img class="logo-footer" src={logoFooter} alt="" />
</footer>

<style lang="scss">
	footer {
		::selection {
			background: rgba(0, 123, 255, 0.2); /* Semi-transparent blue */
			color: #fff; /* Black text for contrast */
			text-shadow: 0 1px 1px rgba(255, 255, 255, 0.5); /* Subtle white shadow for depth */
		}
		width: 100%;
		margin: auto;
		position: relative;
		background: linear-gradient(0deg, rgba(18, 79, 169, 1) 0%, rgba(253, 253, 253, 1) 100%);

		.contact-container {
			position: relative;
			width: 60%;
			margin: 0 auto;
			img {
				position: relative;
				margin: auto;
				z-index: 0;
				max-width: 100%;
				border-radius: 25px;
				box-shadow: 4px 4px 12px 0 rgba(0, 0, 0, 0.5);
			}
			.content {
				position: absolute;
				top: 0;
				font-family: 'Roundo';
				color: var(--white);
				display: flex;
				width: 100%;
				height: 100%;
				justify-content: space-evenly;
				align-items: center;
				.left {
					h1 {
						font-size: var(--fs-700);
					}
				}
				.right {
					ul {
						li {
							list-style-type: none;
							font-size: var(--fs-400);
							margin: 10px 0;
						}
					}
				}
			}
		}
		.social-container {
			width: 70%;
			margin: 50px auto;
			background-color: var(--blue-700);
			border-radius: 15px;
			box-shadow:
				4px 4px 12px 0 rgba(0, 0, 0, 0.25),
				inset 0 4px 12px rgba(255, 255, 255, 0.25);
			color: var(--white);
			font-family: 'Roundo';
			display: flex;
			.left {
				display: flex;
				flex-direction: column;
				justify-content: center;
				gap: 10px;
				width: 100%;
				height: 100%;
				margin: 2.5%;
				p {
					font-size: var(--fs-400);
				}
				ul {
					display: flex;
					gap: 5%;
					li {
						list-style-type: none;
						font-size: var(--fs-400);
					}
				}
			}
			.right {
				width: 100%;

				ul {
					align-items: center;
					justify-content: end;
					padding-right: 20px;
					display: flex;
					height: 100%;
					li {
						list-style-type: none;
						margin: 025px;
						font-size: var(--fs-400);
					}
				}
			}
		}

		.logo-footer {
			width: fit-content;
			width: 100%;
			mix-blend-mode: screen;
		}

		// height: 50vh;
		// background-image: radial-gradient(var(--blue-300) 20px, var(--white) 10px);
		// background-size: 5vw 5vw;
	}
</style>

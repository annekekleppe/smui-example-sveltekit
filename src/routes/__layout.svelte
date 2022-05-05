<script lang="ts">
	import Button from '@smui/button';
	import type { TopAppBarComponentDev } from '@smui/top-app-bar';
	import TopAppBar, { Row, Section, Title, AutoAdjust } from '@smui/top-app-bar';
	import IconButton from '@smui/icon-button';
	import { Label, Icon } from '@smui/common';
	import { Svg } from '@smui/common/elements';
	import { mdiGithub, mdiWeb } from '@mdi/js';
	import Tooltip, { Wrapper } from '@smui/tooltip';

	let topAppBar: TopAppBarComponentDev;

	let lightTheme =
		typeof window === 'undefined' || window.matchMedia('(prefers-color-scheme: light)').matches;
	function switchTheme() {
		lightTheme = !lightTheme;
		let themeLink = document.head.querySelector<HTMLLinkElement>('#theme');
		if (!themeLink) {
			themeLink = document.createElement('link');
			themeLink.rel = 'stylesheet';
			themeLink.id = 'theme';
		}
		themeLink.href = `/smui${lightTheme ? '' : '-dark'}.css`;
		document.head
			.querySelector<HTMLLinkElement>('link[href$="/smui-dark.css"]')
			?.insertAdjacentElement('afterend', themeLink);
	}
</script>

<TopAppBar bind:this={topAppBar} variant="standard">
	<Row>
		<Section>
			<Title>My App</Title>
		</Section>
		<Section align="end" toolbar>
			<IconButton aria-label="GitHub" href="https://github.com/hperrin/svelte-material-ui">
				<Icon component={Svg} viewBox="0 0 24 24">
					<path fill="currentColor" d={mdiGithub} />
				</Icon>
			</IconButton>

			<Wrapper>
				<IconButton aria-label="Demo Site" href="https://sveltematerialui.com">
					<Icon component={Svg} viewBox="0 0 24 24">
						<path fill="currentColor" d={mdiWeb} />
					</Icon>
				</IconButton>
				<!--
					Note: the toolip element in a simple
					tooltip is hoisted up to the body element.
				-->
				<Tooltip>Tooltip on a button 3.</Tooltip>
			</Wrapper>
		</Section>
	</Row>
</TopAppBar>

<AutoAdjust {topAppBar} style="display: flex; justify-content: space-between;">
	<div class="container"><slot /></div>
	<div class="container">
		<Wrapper rich>
			<Button on:click={switchTheme}>
				<Label>{lightTheme ? 'Lights off' : 'Lights on'}</Label>
			</Button>
			<!--
				Note: the toolip element in a simple
				tooltip is hoisted up to the body element.
			-->
			<Tooltip>Tooltip on a button 2.</Tooltip>
		</Wrapper>

	</div>
</AutoAdjust>

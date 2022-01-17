<script lang="ts">
	export let webpSrc: string;
	export let fallbackSrc: string;
	export let alt = "";
</script>

<picture>
	<source srcset={webpSrc} type="image/webp" />
	<img src={fallbackSrc} {alt} />
</picture>

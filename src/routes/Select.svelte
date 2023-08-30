<script>
	export let value = '';
</script>

<select
  {...$$restProps}
	bind:value
>
	<slot />
</select>
<template>
	<div class="text-center">
    	<boolean-icon :value="field.value" />
  	</div>
</template>

<script>
export default {
    props: ['resourceName', 'field'],
}
</script>

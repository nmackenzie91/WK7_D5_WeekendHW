<template>
    <div>
        <i><h3>"{{quoteDisplay.en}}"</h3></i>
        <p>- {{quoteDisplay.author}}</p>
    </div>
</template>

<script>
export default {
    name: "quote-comp",
    props: ["quoteDisplay"]
}
</script>

<style>

</style>
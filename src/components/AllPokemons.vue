<template>

    <div>
        <h1>{{ num + 1 }} {{ name }}  </h1>
        <small>{{ url }}</small>
    </div>
      
</template>

<script>
export default {
    props: {
        name: String,
        num: Number,
        url: String
    }
};
</script>

<style scoped>

</style>
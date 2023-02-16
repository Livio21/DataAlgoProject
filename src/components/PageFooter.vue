<template>
    <div>
        <div class="text-xl text-slate-700 font-bold mx-auto">
            <span>Project done by <span class="name bg-clip-text text-transparent bg-gradient-to-r
                     from-blue-500 via-emerald-500 to-teal-600">
                    Livio Macaj</span></span>
        </div>
    </div>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
.name {
    background-size: 200% auto;
    color: #000;
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;

    animation: shine 2s ease-out infinite;

    @keyframes shine {
        to {
            background-position: 200% center;
        }
    }
}
</style>
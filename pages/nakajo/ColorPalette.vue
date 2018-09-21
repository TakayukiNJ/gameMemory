<template>
    <div class="palette">
        <div
            v-for="color in list"
            :key="color"
            :style="`background-color: ${color}`"
        >
        </div>
    </div>
</template>

<script>
export default {
  props: ['list', 'current'],
};
</script>

<style>
.pallet {
    position: fixed;
    bottom: 0;
    right: 0;
    background: #fff;
    width: 100px;
}

.palette > div {
    box-sizing: border-box;
    width: 50%;
    height: 50px;
    border-radius: 5px;
    border: 2px;
    display: inline-block;
    cursor: pointer;
}

.palette > div:hover{
    border-color: #ff0;
}

</style>

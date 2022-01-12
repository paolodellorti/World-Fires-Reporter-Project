<template>
    <div class="controller">
        <button @click="deselectAll">Deselect All</button>
        <h2 v-if="days === 1">{{ fires }} fires in {{ days }} day</h2>
        <h2 v-else-if="days">{{ fires }} fires in {{ days }} days</h2>
        <h2 v-else>No days selected</h2>
        <button @click="selectAll">Select All</button>
    </div>
</template>

<script>
export default {
    name: "ControllerItem",
    props: {
        fires: {
            type: Number
        },
        days: {
            type: Number
        }
    },
    methods: {
        deselectAll() {
            document.querySelectorAll('.bar').forEach(bar => bar.classList.add("deselected"))
            this.$emit('changeFilter', 'deselectAll')
        },
        selectAll() {
            document.querySelectorAll('.bar').forEach(bar => bar.classList.remove("deselected"))
            this.$emit('changeFilter', 'selectAll')
        }    
    }
}
</script>

<style scoped>
    .controller {
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin: 0 auto;
        width: 70%;
    }
    button {
        padding: 1%;
        background-color: crimson;
        border: none;
        border-radius: 5px;
        color: white;
        transition: all 0.2s;
        font-family: 'Oswald', sans-serif;
    }
    button:hover {
        background-color: #da4f6b;
        transition: all 0.2s;
    }
</style>
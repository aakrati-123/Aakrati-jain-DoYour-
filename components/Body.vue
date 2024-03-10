<template>
    <div class="body">
        <Status 
            v-for="status, i in totalStatus" 
            :key="i" 
            :status="status" 
        />
    </div>
</template>

<script>
    import {mapState} from 'vuex'

    export default {
        computed: {
            ...mapState(['totalStatus'])
        }
    }
</script>

<style scoped>
.body{
    min-height: 100%;
    display: flex;
    justify-content: center;
    margin-top: 15rem;
}
</style>
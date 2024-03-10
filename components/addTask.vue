<template>
    <div class="edit-task">
        <NuxtLink to="/"><svg xmlns="http://www.w3.org/2000/svg" class="back-icon" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
        </svg></NuxtLink>
        <h2 class="heading">Add a Task</h2>
        <form class='form'>
            <label for="task_name">Name:</label>
            <input type="text" id="task_name" v-model="task_name" required class="name-input"/>
            <br/>

            <label for="task_description">Description:</label>
            <textarea id="task_description" v-model="task_description" class="desc-input" rows="6"></textarea>
            <br/>

            <label for="task_status">Status:</label>
            <label v-if="status">{{status}}</label> 
            <select v-else v-model="task_status" id="task_status">
                <option value="status" >Status</option>
            </select>
            <br/>

            <button @click="addTaskHandler" class="submit-btn">
                Submit
            </button>
        </form>
    </div>
</template>

<script>
    import { mapMutations } from 'vuex';

    export default {
        props: ['status'],
        data() {
            return {
                task_name: "",
                task_description: "",
                task_status: "" // Assuming you want to bind task_status to a select
            }
        },
        methods: {
            ...mapMutations(['addTask']),
            addTaskHandler() {
                this.addTask({
                    task: this.task_name,
                    description: this.task_description,
                    status: this.task_status,
                    id: Math.floor((Math.random() * 100) + 1)
                });

                this.$nuxt.$options.router.push(`/`);
            }
        }
    }
</script>

<style scoped>
.edit-task {
    display: flex;
    flex-direction: column;
    margin: 2rem auto;
    padding: 1rem;
    max-width: 400px;
    border: 1px solid #ccc;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    background-image: url('https://th.bing.com/th/id/OIP.hV4R2t0aexY8oYSLvr7TcAHaFj?w=1024&h=768&rs=1&pid=ImgDetMain');
    background-size: cover;
    background-position: center;
}

.heading {
    text-align: center;
    margin-bottom: 1rem;
    font-size: 1.5rem;
}

.back-icon {
    height: 20px;
    width: 20px;
    fill: #333;
    margin-right: 0.5rem;
}

.form {
    display: flex;
    flex-direction: column;
}

label {
    font-weight: bold;
}

input[type="text"],
textarea,
select {
    width: 100%;
    padding: 0.5rem;
    margin-bottom: 1rem;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
}

.submit-btn {
    width: 100%;
    padding: 0.8rem;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.submit-btn:hover {
    background-color: #0056b3;
}
</style>

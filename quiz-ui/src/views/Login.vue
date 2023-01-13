<template>
    <div>
        <h1>
            Admin
        </h1>
        <div class="register">
            <input type="password" v-model="password" placeholder="Enter Password" />
            <button v-on:click="Connect">Login</button>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
    data() {
        return {
            password: "",
        }
    },
    created() {
    
    },
    methods: {
        async Connect() {
            const response = await axios.post('http://127.0.0.1:5000/login', {
                password: this.password
            });
            const status = response.status;
            if (status === 401) {
                this.showErrorMsg = true;
            }
            else {
                const token = response.data["token"];
                localStorage.setItem("token", token);
                this.$router.push('/admin');
                console.log(token);
            }
        }
    }
}
</script>

<script>
export default {
    data() {
        return {
            username: '',
            password: '',
        }
    },
    methods: {

        s(){
            if(this.username !== 'Stockly' || this.password !== '123'){
                alert('Incorrect Password or Username');
                this.username = '';
                this.password = '';

            }
            else if(this.username === 'Stockly' && this.password === '123'){
                alert('Log in Successfully');
                this.$emit('loginS', 'Dashboard');
            }
        }
    }
}
</script>

<template>
    <section
        class=" w-full h-screen bg-linear-to-b from-blue-700 via-blue-600 to-blue-500 flex justify-center items-center">
        <div class="w-full max-w-xs m-auto bg-indigo-100 rounded p-5">
            <header>
                <img class="w-20 mx-auto mb-5 animate-pulse" src="https://img.icons8.com/fluent/344/year-of-tiger.png" />
            </header>
            <form>
                <div>
                    <label class="block mb-2 text-indigo-500" >Username</label>
                    <input v-model="username"
                        class="w-full p-2 mb-6 text-indigo-700 border-b-2 border-indigo-500 outline-none focus:bg-gray-300"
                        type="text" >
                </div>
                <div>
                    <label class="block mb-2 text-indigo-500" >Password</label>
                    <input v-model="password"
                        class="w-full p-2 mb-6 text-indigo-700 border-b-2 border-indigo-500 outline-none focus:bg-gray-300"
                        type="text" >
                </div>
                <div>
                    <button @click="s" class="w-full bg-indigo-700 hover:bg-blue-700 text-white font-bold py-2 px-4 mb-6 rounded" 
                        >Submit</button>
                </div>
            </form>
            <footer>
                <a class="text-indigo-700 hover:text-pink-700 text-sm float-left" >Forgot Password?</a>
                <a class="text-indigo-700 hover:text-pink-700 text-sm float-right" >Create Account</a>
            </footer>
        </div>
    </section>
</template>
<template>
    <button @click="toggleVisiblity" class="relative flex items-center">
        <img
            class="h-10 w-10 object-cover rounded mr-2"
            src="https://images.unsplash.com/photo-1580489944761-15a19d654956?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1361&q=80"
            alt="Current profile photo"
        />
        <p class="text-black text-lg font-semibold">Jonas Smit</p>
        <div
            v-if="isVisible"
            class="absolute mt-2 w-36 left-4 top-8 bg-white rounded-md shadow-xl z-50 text-center"
        >
            <RouterLink
                to="/profil"
                class="block px-4 py-2 text-sm capitalize hover:bg-rose-200"
            >Profil</RouterLink>
            <RouterLink to="/" class="block px-4 py-2 text-sm capitalize hover:bg-rose-200">Log out</RouterLink>
        </div>
    </button>
</template>

<script>
export default {
    data() {
        return {
            isVisible: false
        };
    },
    methods: {
        toggleVisiblity() {
            this.isVisible = !this.isVisible;
        }
    }
};
</script>

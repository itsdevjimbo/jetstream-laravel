<template>
    <header
        class="flex justify-between items-center py-4 px-6 bg-white border-b-4 border-indigo-600"
    >
        <div class="flex items-center">
            <button
                @click="toggleSidebar()"
                class="text-gray-500 focus:outline-none lg:hidden"
            >
                <svg
                    class="h-6 w-6"
                    viewBox="0 0 24 24"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <path
                        d="M4 6H20M4 12H20M4 18H11"
                        stroke="currentColor"
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                    />
                </svg>
            </button>

            <div class="relative mx-4 lg:mx-0">
                <span class="absolute inset-y-0 left-0 pl-3 flex items-center">
                    <svg
                        class="h-5 w-5 text-gray-500"
                        viewBox="0 0 24 24"
                        fill="none"
                    >
                        <path
                            d="M21 21L15 15M17 10C17 13.866 13.866 17 10 17C6.13401 17 3 13.866 3 10C3 6.13401 6.13401 3 10 3C13.866 3 17 6.13401 17 10Z"
                            stroke="currentColor"
                            stroke-width="2"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        />
                    </svg>
                </span>

                <input
                    class="w-32 sm:w-64 rounded-md pl-10 pr-4 focus:border-indigo-600"
                    type="text"
                    placeholder="Search"
                />
            </div>
        </div>

        <div class="flex items-center">
            <div class="relative">
                <button
                    @click="dropdownOpen = !dropdownOpen"
                    class="relative z-10 block h-8 w-8 rounded-full overflow-hidden shadow focus:outline-none"
                >
                    <img
                        class="h-full w-full object-cover"
                        :src="
                            $page.props.user.profile_photo_url
                                ? $page.props.user.profile_photo_url
                                : 'https://images.unsplash.com/photo-1528892952291-009c663ce843?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=296&q=80'
                        "
                        alt="Your avatar"
                    />
                </button>

                <div
                    v-show="dropdownOpen"
                    @click="dropdownOpen = false"
                    class="fixed inset-0 h-full w-full z-10"
                ></div>

                <div
                    v-show="dropdownOpen"
                    class="absolute right-0 mt-2 py-2 w-48 bg-white rounded-md shadow-xl z-20"
                >
                    <inertia-link
                        :href="route('profile.show')"
                        :active="route().current('profile.show')"
                        as="button"
                        type="button"
                        class="w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-indigo-600 hover:text-white w-max"
                    >
                        Profile
                    </inertia-link>
                    <form method="POST" @submit.prevent="logout">
                        <button
                            type="submit"
                            class="w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-indigo-600 hover:text-white w-max"
                        >
                            Logout
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </header>
</template>

<script>
// import Button from "../../Components/Button.vue";
import JetResponsiveNavLink from "@/Jetstream/ResponsiveNavLink";
export default {
    // components: { JetResponsiveNavLink },
    data: () => ({
        dropdownOpen: false,
    }),
    methods: {
        logout() {
            this.$inertia.post(route("logout"));
        },
        toggleSidebar() {
            this.emitter.emit("sidebar-changed");
        },
    },
};
</script>

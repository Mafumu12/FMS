<script setup>
import {  FaArrowLeft, FaChartPie, FaChevronDown, FaCubes, FaSeedling } from 'vue3-icons/fa';
import { ref } from 'vue';
import { Link } from '@inertiajs/vue3';

const isDashboardDropdownOpen = ref(false);
const isModulesDropdownOpen = ref(false);
const isMobileNavOpen = ref(false);
const toggleMobileNav = () => {
    isMobileNavOpen.value = !isMobileNavOpen.value;
};

const toggleDropdown = (dropdown) => {
    if (dropdown === 'dashboard') {
        isDashboardDropdownOpen.value = !isDashboardDropdownOpen.value;
    } else if (dropdown === 'modules') {
        isModulesDropdownOpen.value = !isModulesDropdownOpen.value;
    }
};
</script>

<template>

    <nav class="bg-white   fixed w-full z-20 top-0 start-0 border-b border-gray-200  ">
        <button @click="toggleMobileNav" type="button"
            class="inline-flex items-center justify-center p-2 w-10 h-10 text-sm text-[#EBE9EB] rounded-lg hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200"
            aria-controls="navbar-hamburger" :aria-expanded="isMobileNavOpen.toString()">

            <svg v-if="!isMobileNavOpen" class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg"
                fill="none" viewBox="0 0 17 14">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M1 1h15M1 7h15M1 13h15" />
            </svg>


        </button>

    </nav>
    <aside
        class="fixed left-0 top-0 h-screen w-72.5  bg-[#17594A] transform transition-transform duration-300 ease-in-out z-50 md:translate-x-0"
        :class="{ 'translate-x-0': isMobileNavOpen, '-translate-x-full': !isMobileNavOpen }">
        <div class="flex items-center justify-between gap-1 px-6 py-5.5 lg:py-6.5">
            <router-link to="/">
                <div class="flex items-center gap-2">
                    <span class="text-[#D1CF4F] text-[36px]">
                        <FaSeedling />
                    </span>
                    <span class="text-[#EBE9EB] text-[32px] font-medium">Agro</span>
                </div>
            </router-link>
            <button @click="toggleMobileNav" type="button" class="block lg:hidden">
                <span class=" text-[#F4F4F4] font-light">
                    <FaArrowLeft />
                </span>
            </button>
        </div>

        <div class="no-scrollbar flex flex-col overflow-y-auto">
            <nav class="mt-5 py-4 px-4 lg:mt-9 lg:px-6">

                <h3 class="mb-4 ml-2  text-sm font-normal text-[#F4F4F4]">MENU</h3>
                <ul class="mb-6 flex flex-col gap-1.5">


                    <li>
                        <button @click="toggleDropdown('dashboard')" type="button"
                            class="flex items-center w-full p-2 text-base bg-[#467A6E] text-gray-900 transition duration-75 rounded-lg">
                            <span class="text-[#F4F4F4] text-[20px] md:text-[24px]">
                                <FaChartPie />
                            </span>
                            <span
                                class="flex-1 ms-3 text-left rtl:text-right text-[#EBE9EB] text-[14px] md:text-[18px]  whitespace-nowrap">Dashboard</span>
                            <span class="text-[#F4F4F4] text-[12px] md:text-[16px]">
                                <FaChevronDown />
                            </span>
                        </button>
                        <ul v-if="isDashboardDropdownOpen" class="py-2 space-y-2">
                            <li>
                                <a href="#"
                                    class="flex items-center w-full p-2 text-white rounded-lg pl-11 hover:text-[#D3C11D] font-thin">Overview</a>
                            </li>
                        </ul>
                    </li>

                    <li class="my-2">
                        <button @click="toggleDropdown('modules')" type="button"
                            class="flex items-center w-full p-2 text-base text-gray-900 transition duration-75 rounded-lg hover:bg-[#467A6E]">
                            <span class="text-[#F4F4F4] text-[20px] md:text-[24px]">
                                <FaCubes />
                            </span>
                            <span
                                class="flex-1 ms-3 text-left rtl:text-right text-[#EBE9EB] text-[14px] md:text-[18px] whitespace-nowrap">Modules</span>
                            <span class="text-[#F4F4F4] text-[12px] md:text-[16px]">
                                <FaChevronDown />
                            </span>
                        </button>
                        <ul v-if="isModulesDropdownOpen" class="py-2 space-y-2">
                            <li>
                                <a href="#"
                                    class="flex items-center w-full p-2 text-white rounded-lg pl-11   hover:text-[#D3C11D] font-thin">Install</a>
                            </li>
                            <li>
                                <Link href="/upload"
                                    class="flex items-center w-full p-2 text-white rounded-lg pl-11 hover:text-[#D3C11D]   font-thin">Upload</Link>
                            </li>
                        </ul>
                    </li>
                </ul>
            </nav>
        </div>
    </aside>
</template>

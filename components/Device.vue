<template>
    <div>
        <button id="dropdownDeviceButton" data-dropdown-toggle="dropdownDevices" class="display-inline content-center text-black bg-meshtastic hover:bg-gray-200 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center inline-flex items-center" type="button">
            {{ selectedTarget.replace('_', '-') }}
            <svg class="w-2.5 h-2.5 ms-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 4 4 4-4"/>
            </svg>
        </button>
        <div id="dropdownDevices" class="z-10 hidden bg-gray-200 divide-y divide-gray-500 rounded-lg shadow w-52">
            <div id="accordion-esp" data-accordion="collapse">
                <span id="accordion-esp-heading">
                    <button type="button" class="flex items-center justify-between w-full p-3 font-medium rtl:text-right text-gray-500 border border-b-0 border-gray-200 rounded-t-xl focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-800 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800 gap-3" data-accordion-target="#accordion-esp-body" aria-expanded="true" aria-controls="accordion-esp-body">
                    <span class="flex items-center">
                        <img src="@/assets/img/espressif.svg" class="w-32 inline-block" />
                    </span>
                    <svg data-accordion-icon class="w-3 h-3 rotate-180 shrink-0" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5 5 1 1 5"/>
                    </svg>
                    </button>
                </span>
            </div>
            <ul id="accordion-esp-body" aria-labelledby="accordion-esp-heading" class="text-xs text-gray-900">
                <li v-for="target in store.$state.targets.filter(h => h.architecture.includes('esp')).sort((a, b) => a.displayName.localeCompare(b.displayName))">
                    <a class="block px-4 py-1 hover:bg-gray-400 cursor-pointer" @click="setTarget(target)">
                        {{ target.displayName }}
                    </a>
                </li>
            </ul>
            <div id="accordion-nordic" data-accordion="collapse">
                <span id="accordion-nordic-heading">
                    <button type="button" class="flex items-center justify-between w-full p-3 font-medium rtl:text-right text-gray-500 border border-b-0 border-gray-200 rounded-t-xl focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-800 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800 gap-3" data-accordion-target="#accordion-nordic-body" aria-expanded="true" aria-controls="accordion-esp-body">
                    <span class="flex items-center">
                        <img src="@/assets/img/nordic.svg" class="w-32 inline-block" />
                    </span>
                    <svg data-accordion-icon class="w-3 h-3 rotate-180 shrink-0" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5 5 1 1 5"/>
                    </svg>
                    </button>
                </span>
            </div>
            <ul id="accordion-nordic-body" aria-labelledby="accordion-nordic-heading" class="text-xs text-gray-900">
                <li v-for="target in store.$state.targets.filter(h => h.architecture.includes('nrf')).sort((a, b) => a.displayName.localeCompare(b.displayName))">
                    <a class="block px-4 py-1 hover:bg-gray-400 cursor-pointer" @click="setTarget(target)">
                        {{ target.displayName }}
                    </a>
                </li>
            </ul>
            <div id="accordion-rp2040" data-accordion="collapse">
                <span id="accordion-rp2040-heading">
                    <button type="button" class="flex items-center justify-between w-full p-3 font-medium rtl:text-right text-gray-500 border border-b-0 border-gray-200 rounded-t-xl focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-800 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800 gap-3" data-accordion-target="#accordion-rp2040-body" aria-expanded="true" aria-controls="accordion-esp-body">
                    <span class="flex items-center">
                        <img src="@/assets/img/rp2040.svg" class="w-32 inline-block" />
                    </span>
                    <svg data-accordion-icon class="w-3 h-3 rotate-180 shrink-0" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5 5 1 1 5"/>
                    </svg>
                    </button>
                </span>
            </div>
            <ul id="accordion-rp2040-body" aria-labelledby="accordion-rp2040-heading" class="py-2 text-xs text-gray-900">
                <li v-for="target in store.$state.targets.filter(h => h.architecture.includes('rp2040')).sort((a, b) => a.displayName.localeCompare(b.displayName))">
                    <a class="block px-4 py-1 hover:bg-gray-400 cursor-pointer" @click="setTarget(target)">
                        {{ target.displayName }}
                    </a>
                </li>
            </ul>
        </div>
        <button data-tooltip-target="tooltip-auto" class="mx-2 display-inline content-center px-3 py-2 text-xs font-medium text-center  hover:bg-gray-200 focus:ring-4 focus:outline-none focus:ring-blue-300 rounded-lg inline-flex items-center text-white hover:text-black"
            type="button"
            @click="store.autoSelectHardware">
            <SparklesIcon class="h-4 w-4" :class="{'animate-bounce': !store.$state.selectedTarget?.hwModel }" />
        </button>
        <div id="tooltip-auto" role="tooltip" class="absolute z-10 invisible inline-block px-3 py-2 text-sm font-medium text-white transition-opacity duration-300  rounded-lg shadow-sm opacity-0 tooltip bg-gray-700">
            Attempt to automatically select the device type if Meshtastic > (2.1.X) is already installed.
            <div class="tooltip-arrow" data-popper-arrow></div>
        </div>
    </div>
</template>

<script lang="ts" setup>
import type { DeviceHardware } from '~/types/api';

import { SparklesIcon } from '@heroicons/vue/24/solid';

import { useDeviceStore } from '../stores/deviceStore';

const store = useDeviceStore();
store.fetchList();

const selectedTarget = computed(() => store.$state.selectedTarget?.hwModel ? store.$state.selectedTarget?.displayName : "Select Target Device")

const setTarget = (target: DeviceHardware) => {
    store.setSelectedTarget(target);
    document.getElementById('dropdownDevices')?.classList.toggle('hidden');
}

</script>
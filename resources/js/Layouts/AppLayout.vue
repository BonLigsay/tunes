<script setup lang="ts">
import { ref, onMounted, onUnmounted, computed } from 'vue';
import SidebarLink from '@/Components/SidebarLink.vue';
import { Link } from '@inertiajs/vue3';

const showingNavigationDropdown = ref(false);

const showDropdown0 = ref(false);
const showDropdown1 = ref(false);
const showDropdown2 = ref(false);
const showDropdown3 = ref(false);
const showDropdown4 = ref(false);

const activeDropdown0 = ref(false);
const activeDropdown1 = ref(false);
const activeDropdown2 = ref(false);
const activeDropdown3 = ref(false);
const activeDropdown4 = ref(false);

const showSidebar = ref(false);

</script>
<template>
    <div class="antialiased">
    <!-- Sidebar -->
    <aside 
      class="fixed left-0 z-40 w-12 h-screen transition-all bg-white border-r border-gray-200 dark:bg-gray-800 dark:border-gray-700"
      aria-label="Sidenav"
      id="drawer-navigation"
      :class="[
        showSidebar ? 'w-64' :''
      ]"
    >      
      <div class="py-5 px-2 h-full bg-white dark:bg-gray-800">
        <div class="flex justify-content items-center text-xl text-right text-white font-medium">
              <button 
                @click="showSidebar = !showSidebar"
                data-drawer-target="drawer-navigation"
                data-drawer-toggle="drawer-navigation"
                aria-controls="drawer-navigation"
                class="p-1 pl-1 text-gray-600 rounded-lg cursor-pointer hover:text-gray-900 hover:bg-gray-100 focus:bg-gray-100 dark:focus:bg-gray-700 focus:ring-2 focus:ring-gray-100 dark:focus:ring-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white"
              >
                <svg
                  aria-hidden="true"
                  class="w-6 h-6"
                  :class="[
                    showSidebar ? 'hidden' : ''
                  ]"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    fill-rule="evenodd"
                    d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h6a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z"
                    clip-rule="evenodd"
                  ></path>
                </svg>

                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6" :class="[
                  !showSidebar ? 'hidden' : ''
                ]">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 12h-15m0 0l6.75 6.75M4.5 12l6.75-6.75" />
                </svg>

                <span class="sr-only">Toggle sidebar</span>
              </button>
            <div class="flex-1 ml-3 text-right whitespace-nowrap4" :class="[
              !showSidebar ? 'hidden' : ''
            ]">
              {{ $page.props.auth.user.name }}
            </div>
          </div>
        <ul class="pt-5 mt-5 space-y-2 py-1 border-t border-gray-200 dark:border-gray-700">
          <!-- Dashboard -->
          <li>
            <SidebarLink href="/dashboard"
              class="flex items-center p-2 pl-1 text-base font-medium text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700 group"
            >
              <svg
                aria-hidden="true"
                class="flex-shrink-0 w-6 h-6 text-gray-500 transition duration-75 group-hover:text-gray-900 dark:text-gray-400 dark:group-hover:text-white"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path d="M2 10a8 8 0 018-8v8h8a8 8 0 11-16 0z"></path>
                <path d="M12 2.252A8.014 8.014 0 0117.748 8H12V2.252z"></path>
              </svg>
              <span class="flex-1 ml-3 text-left whitespace-nowrap" :class="[
                !showSidebar ? 'hidden' : ''
              ]"
                    >Dashboard</span
                  >
            </SidebarLink>
          </li>
          <!-- Requests -->
          <li>
            <SidebarLink
              :href="route('requests')"
              class="flex items-center p-2 pl-1 w-full text-base font-medium text-gray-900 rounded-lg transition duration-75 group hover:bg-gray-100 dark:text-white dark:hover:bg-gray-700"
            >
              <svg
                  aria-hidden="true"
                  class="flex-shrink-0 w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path d="M9 2a1 1 0 000 2h2a1 1 0 100-2H9z"></path>
                  <path
                    fill-rule="evenodd"
                    d="M4 5a2 2 0 012-2 3 3 0 003 3h2a3 3 0 003-3 2 2 0 012 2v11a2 2 0 01-2 2H6a2 2 0 01-2-2V5zm3 4a1 1 0 000 2h.01a1 1 0 100-2H7zm3 0a1 1 0 000 2h3a1 1 0 100-2h-3zm-3 4a1 1 0 100 2h.01a1 1 0 100-2H7zm3 0a1 1 0 100 2h3a1 1 0 100-2h-3z"
                    clip-rule="evenodd"
                  ></path>
                </svg>
              <span class="flex-1 ml-3 text-left whitespace-nowrap" :class="[
                !showSidebar ? 'hidden' : ''
              ]">Requests</span>
            </SidebarLink>
          </li>
          <!-- Reports -->
          <li>
            <SidebarLink              
              class="flex items-center p-2 pl-1 w-full text-base font-medium text-gray-900 rounded-lg transition duration-75 group hover:bg-gray-100 dark:text-white dark:hover:bg-gray-700"
            >
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="flex-shrink-0 w-6 h-6 text-gray-500 transition duration-75 group-hover:text-gray-900 dark:text-gray-400 dark:group-hover:text-white">
                <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 3v11.25A2.25 2.25 0 006 16.5h2.25M3.75 3h-1.5m1.5 0h16.5m0 0h1.5m-1.5 0v11.25A2.25 2.25 0 0118 16.5h-2.25m-7.5 0h7.5m-7.5 0l-1 3m8.5-3l1 3m0 0l.5 1.5m-.5-1.5h-9.5m0 0l-.5 1.5m.75-9l3-3 2.148 2.148A12.061 12.061 0 0116.5 7.605" />
              </svg>
              <span class="flex-1 ml-3 text-left whitespace-nowrap" :class="[
                !showSidebar ? 'hidden' : ''
              ]">Reports</span>
            </SidebarLink>
          </li>
          <!--admin-->
          <li>
            <button
              type="button"
              class="flex items-center p-2 pl-1 w-full text-base font-medium text-gray-900 rounded-lg transition duration-75 group hover:bg-gray-100 dark:text-white dark:hover:bg-gray-700"
              aria-controls="dropdown-authentication"
              data-collapse-toggle="dropdown-authentication"
              @click="showDropdown0 = !showDropdown0, showDropdown1 = false, showDropdown2 = false, showDropdown3 = false, showDropdown4 = false"
              :class="[
                    showDropdown0 
                ]"
            >
              <svg
                aria-hidden="true"
                class="flex-shrink-0 w-6 h-6 text-gray-500 transition duration-75 group-hover:text-gray-900 dark:text-gray-400 dark:group-hover:text-white"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  fill-rule="evenodd"
                  d="M5 9V7a5 5 0 0110 0v2a2 2 0 012 2v5a2 2 0 01-2 2H5a2 2 0 01-2-2v-5a2 2 0 012-2zm8-2v2H7V7a3 3 0 016 0z"
                  clip-rule="evenodd"
                ></path>
              </svg>
              <span class="flex-1 ml-3 text-left whitespace-nowrap" :class="[
                !showSidebar ? 'hidden' : ''
              ]"
                >Admin</span
              >
              <svg
                aria-hidden="true"
                class="w-6 h-6"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  fill-rule="evenodd"
                  d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                  clip-rule="evenodd"
                ></path>
              </svg>
            </button>
            <ul id="dropdown-authentication" class="z-50 absolute w-60 overflow-y-auto py-2 text-sm text-gray-700 dark:text-gray-200 rounded" 
            v-show="showDropdown0" 
                :class="[
                        showDropdown0 ? 'bg-gradient-to-r from-gray-400 to-gray-300' : ''
                    ]">
              <span :class="[
                showSidebar ? 'hidden' : ''
              ]" class="flex items-center justify-center font-bold border-b pb-2 w-full text-base text-gray-900 rounded-lg transition duration-75 group">Admin</span>
              <li>
                <SidebarLink
                
                  class="flex items-center h-1 border-b pt-4 p-2 pl-11 w-full text-sm font-medium text-gray-900 rounded-lg transition duration-75 group hover:bg-gray-100 dark:text-white dark:hover:bg-gray-700"
                  >Users</SidebarLink
                >
              </li>
              <li>
                <SidebarLink
                  
                  class="flex items-center h-1 border-b pt-4 p-2 pl-11 w-full text-sm font-medium text-gray-900 rounded-lg transition duration-75 group hover:bg-gray-100 dark:text-white dark:hover:bg-gray-700"
                  >Roles</SidebarLink
                >
              </li>
              <li>
                <SidebarLink
                   
                  class="flex items-center h-1 border-b pt-4 p-2 pl-11 w-full text-sm font-medium text-gray-900 rounded-lg transition duration-75 group hover:bg-gray-100 dark:text-white dark:hover:bg-gray-700"
                  >permission</SidebarLink
                >
              </li>          
            </ul>
          </li>
        </ul>
        <ul class="pt-5 mt-5 space-y-2 py-1 border-t border-gray-200 dark:border-gray-700 ">
          <li>
            <Link :href="route('logout')" method="post" as="button"
                class="flex items-center p-2 pl-1 w-full text-base font-medium text-gray-900 rounded-lg transition duration-75 group hover:bg-gray-100 dark:text-white dark:hover:bg-gray-700">
            <svg xmlns="http://www.w3.org/2000/svg" class="flex-shrink-0 w-6 h-6 text-gray-500 transition duration-75 group-hover:text-gray-900 dark:text-gray-400 dark:group-hover:text-white" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width=""
                    d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
            </svg>
            <span class="flex-1 ml-3 text-left whitespace-nowrap" :class="[
              !showSidebar ? 'hidden' : ''
            ]">Logout</span>
            </Link>
          </li>
        </ul>  
        <ul class="pt-5 mt-5 space-y-2 py-1 border-gray-200 dark:border-gray-700">
          <li class="hidden md:flex items-center justify-center mt-16">
          <!-- <img
            src="/LOGO QUEEN J.png"
            class="w-56 absolute z-0"
            :class="[
              !showSidebar ? 'hidden' : ''
            ]"
          /> -->
          </li>
        </ul>      
      </div>      
    </aside>

    <main @click="showDropdown4 = false, showDropdown0 = false, showDropdown2 = false, showDropdown3 = false, showDropdown1 = false" class="overflow-auto py-4 w-auto h-auto ml-14">
      <div @click="showSidebar = !showSidebar, showDropdown4 = false, showDropdown0 = false, showDropdown2 = false, showDropdown3 = false, showDropdown1 = false" class="fixed inset-0 transition-opacity" :class="[
        !showSidebar ? 'hidden' : ''
      ]">
          <div class="absolute inset-0 bg-gray-500 opacity-75"></div>
      </div>
      <slot/> 
    </main>
  </div>
</template>


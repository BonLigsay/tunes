<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import Welcome from '@/Components/Welcome.vue';
</script>

<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Dashboard
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <main class="p-4 h-auto">
                        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 mb-4">
                            <div  class="flex flex-col gap-4 justify-center items-center border-2 border-dashed border-gray-300 rounded-lg dark:border-gray-600 h-32 md:h-64">
                                <div>
                                    Welcome {{ $page.props.auth.user.name }}
                                </div>
                                <div>
                                    You have new Requests:
                                </div>
                                <div>
                                    3 new requests, due in 3 days
                                </div>                
                            </div>
                            <!--  -->
                            <div class="flex flex-col gap-4 justify-center items-center border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-32 md:h-64">
                                <img src="/images/graph.png"/>
                            </div>
                            <!--  -->
                            <div class="flex flex-col gap-4 justify-center items-center border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-32 md:h-64">
                                <img src="/images/graph1.jpeg"/>
                            </div>
                            <!--  -->
                            <div class="flex flex-col gap-4 justify-center items-center border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-32 md:h-64">
                                <img src="/images/graph2.png"/>
                            </div>
                            <!--  -->  
                        </div>
                    <div class="flex flex-col gap-4 justify-center items-center border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-96 mb-4">
                        
                    </div>
                    <div class="grid grid-cols-2 gap-4 mb-4">
                        <div class="flex flex-col gap-4 justify-center items-center border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-48 md:h-72">
                           
                        </div>
                        <div class="flex flex-col gap-4 justify-center items-center border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-48 md:h-72">
                           
                        </div>
                        <div class="flex flex-col gap-4 justify-center items-center border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-48 md:h-72">
                            
                        </div>
                        <div class="flex flex-col gap-4 justify-center items-center border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-48 md:h-72">
                            
                        </div>
                    </div>
                    <div class="flex flex-col gap-4 justify-center items-center border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-96 mb-4">
                        
                    </div>
                    <div class="grid grid-cols-2 gap-4">
                        <div
                        class="border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-48 md:h-72"
                        ></div>
                        <div
                        class="border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-48 md:h-72"
                        ></div>
                        <div
                        class="border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-48 md:h-72"
                        ></div>
                        <div
                        class="border-2 border-dashed rounded-lg border-gray-300 dark:border-gray-600 h-48 md:h-72"
                        ></div>
                    </div>
                    </main>
                </div>
            </div>
        </div>
    </AppLayout>
</template>

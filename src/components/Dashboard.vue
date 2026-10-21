<!-- DAshboard -->

<script>
export default {
    props: ['totalPrice', 'totalQuantity' , 'myInventory', 'Units'],
    data() {
        return {
            p: 0,
            u: 0, 
        }
    },
    methods: {
        totalUnits(){
            this.u = this.myInventory.length;
        }
    },
    mount(){
        this.totalQuantity()
    }


}
</script>

<template>
    <section class="w-full min-h-screen  bg-gray-100 flex">
        <div class="w-[306px]">

        </div>
        <div class="flex flex-col  w-full">
            <div class="h-[84.8px] w-full">

            </div>
            <div class=" flex flex-col justify-center w-full items-center px-9 py-10">
                <div
                    class="w-[1200px] h-[160px] flex px-10 justify-between items-center rounded-[22px] bg-linear-to-r from-[#4338ca] to-[#7c3aed]">
                    <div class="space-y-2">
                        <p class="font-[500] text-[#e0e7ff] text-[14px]">YOUR BUSINESS ATA GLANCE</p>
                        <h1 class="font-[700] text-[30px] text-white">Manage your stock with confidence.</h1>
                        <p class="font-[500] text-[#e0e7ff] text-[14px]">A simple overview of your products, inventory
                            value, and items that needs restocking.</p>
                    </div>
                    <div class="h-[89.6px] w-[176px] rounded-[16px] bg-[#ffffff1a] border border-[#ffffff33] px-4 py-4 animate-pulse">
                        <p class="text-[14px] text-[#e0e7ff] animate-none">Inventory value</p>
                        <p class="text-[24px] font-[700] text-white animate-none">${{ totalPrice }}</p>
                    </div>
                </div>

                <div class="w-[1200px] flex justify-between">
                    <div class="flex justify-between w-full gap-5 mt-5 ">
                        <div
                            class="w-[600px] h-[157.6px] border-2 border-gray-200 rounded-[16px] bg-white px-5 space-y-4">
                            <div class="flex justify-between items-center py-2">
                                <p class="text-[#64748b] text-[14px] font-[500]">Total products</p>
                                <div
                                    class=" w-[40px] h-[40px] text-center bg-[#eef2ff] rounded-xl flex justify-center items-center">
                                    <p class="text-[#4f46e5]">▤</p>
                                </div>
                            </div>
                            <div>
                                <p class="text-[#1e293b] font-[700] text-[30px]">{{ myInventory.length }}</p>
                                <p class="text-[14px] text-[#64748b]">Unique product items</p>
                            </div>
                        </div>
                        <div
                            class="w-[600px] h-[157.6px] border-2 border-gray-200 rounded-[16px] bg-white px-5 space-y-4">
                            <div class="flex justify-between items-center py-2">
                                <p class="text-[#64748b] text-[14px] font-[500]">Units in stock</p>
                                <div
                                    class=" w-[40px] h-[40px] text-center bg-[#eef2ff] rounded-xl flex justify-center items-center">
                                    <p class="text-[#4f46e5]">▣</p>
                                </div>
                            </div>
                            <div>
                                <p class="text-[#1e293b] font-[700] text-[30px]">{{ totalQuantity }}</p>
                                <p class="text-[14px] text-[#64748b]">Across all products</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </section>
</template> 
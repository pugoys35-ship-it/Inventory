<!-- transactions -->

<script>
export default {
    props: ['user', 'tranArray', 'myt'],
    data() {
        return {

        }
    },
    methods: {

    }
}
</script>

<template>
    <section class="w-full min-h-screen  bg-gray-100 flex">
        <div class="w-[306px]">

        </div>
        <div class="flex flex-col w-full items-center">

            <div
                class="w-[1199.2px] h-[92.8px] flex items-center justify-between border border-gray-300 bg-white rounded-t-[20px] mt-30 px-5">
                <div>
                    <p class="text-[#1e293b] font-[700] text-[18px]">Transactions</p>
                    <p class="text-[14px] text-[#64748b]">View all your transactions's history</p>
                </div>
                <img src="../assets/user.gif" alt="" class="object-contain">
            </div>
            <div
                class="w-[1199.2px] h-[48px] border-r border-l border-b border-gray-300 px-5 grid grid-cols-8 items-center ">
                <p class="col-span-2 font-[600] text-[12px] text-[#64748b]">User</p>

                <p class="text-center font-[600] text-[12px] text-[#64748b]">Product</p>
                <p class="text-center font-[600] text-[12px] text-[#64748b]">Product Name</p>
                <p class="text-center font-[600] text-[12px] text-[#64748b]">PRICE</p>
                <p class="text-center font-[600] text-[12px] text-[#64748b]">QUANTITY</p>
            <div class="flex justify-end px-5 items-center w-full col-span-2">
                <p class=" text-end font-[600] text-[12px] text-[#64748b]">Status</p>
            </div>
            </div>
            <div class="">
                <div class="w-[1199.2px] min-h-[72.4px] bg-white border-r border-l border-b border-gray-300">
                    <div v-for="(item, index) in tranArray" :key="index.id">
                        <div class="flex justify-center items-center h-full py-3 ">
                            <div class=" w-[1199.2px] h-[48px]    px-5 grid grid-cols-8 items-center ">
                                <p class="col-span-2">{{ item.receiverN }}</p>
                                <div class=" flex justify-center items-center w-full">
                                    <p
                                        class=" font-[600] text-[18px] text-[#1e293b] w-fit p-2 rounded-xl bg-[#f1f5f9] ">
                                        {{ item.icon }}
                                    </p>
                                </div>
                                <p class=" text-[14px]  font-[600] text-[#64748b] text-center ">{{ item.name }}</p>

                                <p class=" text-center w-full font-[600] text-[12px] text-[#64748b]">$ <span
                                        class="text-[14px] text-emerald-700">{{ item.price }}</span>
                                </p>
                                <p class=" text-center w-full font-[600] text-[12px] text-[#64748b]"> <span
                           
                                        class="text-[14px] text-emerald-700">{{ item.quantity }}</span>
                                    units</p>


                                <p class="col-span-2 text-end text-emerald-600 font-semibold  rounded-lg ">Completed</p>
                            </div>

                        </div>
                    </div>
                </div>
            </div>
            <div class="w-[1199.2px] h-[50px] border-b border-x border-gray-300 bg-white rounded-b-[20px] px-5 flex items-center">
                <p class="text-[14px] text-[#64748b]">A Total of {{ myt.length }} Transaction<span v-if="myt.length > 1">s</span></p>
            </div>
        </div>
    </section>
</template>

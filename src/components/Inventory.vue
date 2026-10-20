<!-- Inventory -->
<script>

export default {
    props: ['myInventory', 'quantityNum', 'priceNum'],

    data() {
        return {
            minusPrice: null,
            modalT: false,
            transactionIndex: 0,
            mtArray: [],
            receiverName: '',
        }
    },
    methods: {
        deleteProduct(i, u, index) {
            this.$emit('minus', this.minusPrice = i);
            this.$emit('minusQ', this.minusQuantity = u);
            this.myInventory.splice(index, 1);
        },

        showModalT(mt, index) {
            this.modalT = mt;
            this.transactionIndex = index;
            this.mtArray.push(this.myInventory[index])
            console.log(this.mtArray)
        },

        closeModalT(closemt) {
            this.modalT = closemt;
        },

        sendToT() {
            alert('Sent Successfully');
            this.modalT = false;
            this.$emit('addTotrans', this.myInventory[this.transactionIndex])
        },

        cancelmt() {
            this.mtArray = [];
            this.modalT = false;
        },

        sendToTransactions(i, n, c, q,) {
            if (this.receiverName !== '') {
                this.$emit('minusTran', this.minusTranPrice = i);
                this.$emit('minusTranQ', this.minusTranQuantity = q);
                this.myInventory.splice(this.transactionIndex, 1)
                this.$emit('rName', this.receiverName)
                // this.$emit('goTran', this.mtArray[this.transactionIndex]);
                this.$emit('goTran', { receiverN: this.receiverName, price: i, name: n, icon: c, quantity: q });
                this.modalT = false;
                alert('Sent Successfully');
                this.mtArray = [];
                this.receiverName = '';
                this.$emit('page', 'Transactions')
            }

            else{
                alert('Enter User Name')
                
            }

        }
    }
}
</script>

<template>
    <section class="w-full min-h-screen  bg-gray-100 flex">
        <div class="w-[306px]">

        </div>
        <div class="flex flex-col w-full items-center ">

            <div
                class="w-[1199.2px] h-[92.8px] flex items-center  justify-between border border-gray-300 bg-white rounded-t-[20px] mt-30 px-5">
                <div>
                    <p class="text-[#1e293b] font-[700] text-[18px]">Product inventory</p>
                    <p class="text-[14px] text-[#64748b]">View manage all your products</p>
                </div>
                <img src="../assets/bar.gif" alt="">
            </div>
            <div
                class="w-[1199.2px] h-[48px] border-r border-l border-b border-gray-300 px-5 grid grid-cols-8 items-center ">
                <p class="col-span-2 font-[600] text-[12px] text-[#64748b]">PRODUCT</p>

                <p class="text-center font-[600] text-[12px] text-[#64748b]">SKU</p>
                <p class="text-center font-[600] text-[12px] text-[#64748b]">CATEGORY</p>
                <p class="text-center font-[600] text-[12px] text-[#64748b]">PRICE</p>
                <p class="text-center font-[600] text-[12px] text-[#64748b]">QUANTITY</p>

                <p class="col-span-2 text-end font-[600] text-[12px] text-[#64748b] ">ACTION</p>
            </div>
            <div class="">
                <div class="w-[1199.2px] min-h-[72.4px] bg-white border-r border-l border-b border-gray-300">
                    <div v-for="(item, index) in myInventory" :key="index.id">
                        <div class="flex justify-center items-center h-full py-3">
                            <div class=" w-[1199.2px] h-[48px]    px-5 grid grid-cols-8 items-center ">
                                <p class="col-span-2 font-[600] text-[14px] font-[600] text-[#1e293b]"><span
                                        class="p-2 rounded-xl bg-[#f1f5f9] text-[18px]">{{ item.Icon }}</span>{{
                                            item.Name
                                        }}</p>

                                <p class=" text-center w-full font-[600] text-[12px] text-[#64748b]">{{ item.Sku }}</p>
                                <p class=" text-center w-full font-[600] text-[12px] text-[#64748b]">{{ item.Category }}
                                </p>
                                <p class=" text-center w-full font-[600] text-[12px] text-[#64748b]">$ <span
                                        class="text-[14px] text-black">{{ item.Price }}</span>
                                </p>
                                <p class=" text-center w-full font-[600] text-[12px] text-[#64748b]"> <span
                                        class="text-[14px] text-black">{{ item.Quantity }}</span>
                                    units</p>

                                <div class="col-span-2 text-end space-x-5">
                                    <button @click="showModalT(true, index)"
                                        class="text-end text-emerald-600 font-semibold hover:text-emerald-700   cursor-pointer  rounded-lg">Send</button>
                                    <button @click="deleteProduct(item.Price, item.Quantity, index)"
                                        class=" text-end text-red-600 font-semibold hover:text-red-300   cursor-pointer  rounded-lg ">Delete</button>
                                </div>
                            </div>

                        </div>
                    </div>
                </div>
            </div>
            <div class="w-[1199.2px] h-[50px] border-b border-x border-gray-300 bg-white rounded-b-[20px] px-5 flex items-center">
                <p class="text-[#64748b] text-[14px]">Showing {{ myInventory.length }} products in inventory</p>
            </div>
        </div>

        <!-- mt modal -->
        <div v-if="modalT" class="z-20 bg-black/30 fixed w-full h-screen flex justify-center items-center">
            <div class="h-fit w-[612px] bg-white rounded-xl px-5 py-6 space-y-3">
                <div>
                    <h1 class="font-[700] text-[#1e293b] text-[20px]">Add new product</h1>
                    <p class="text-[#64748b] text-[14px]">Enter the product information below.</p>
                </div>
                <div>
                    <p></p>
                </div>
                <div>
                    <h1 class="font-semibold mb-1.5 text-sm">Receiver </h1>
                    <input v-model="receiverName" maxlength="80" placeholder=""
                        class="w-full rounded-xl border border-slate-200 px-3 py-2.5 outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-100 cursor-pointer">
                </div>
                <div class="w-full h-[48px] px-5 grid grid-cols-6 items-center ">
                    <p class="col-span-2 font-[600] text-[12px] text-[#64748b]">PRODUCT</p>

                    <p class="text-center font-[600] text-[12px] text-[#64748b]">SKU</p>
                    <p class="text-center font-[600] text-[12px] text-[#64748b]">CATEGORY</p>
                    <p class="text-center font-[600] text-[12px] text-[#64748b]">PRICE</p>
                    <p class="text-center font-[600] text-[12px] text-[#64748b]">QUANTITY</p>

                </div>

                <div class="w-full w-[1199.2px] min-h-[72.4px] bg-white">
                    <div v-for="(tran, i) in mtArray" :key="i.id">
                        <div class="flex justify-center items-center h-full py-3">
                            <div class=" w-full h-[48px]    px-5 grid grid-cols-6 items-center ">
                                <p class="col-span-2 font-[600] text-[14px] font-[600] text-[#1e293b]"><span
                                        class="p-2 rounded-xl bg-[#f1f5f9] text-[18px]">{{ tran.Icon }}</span>{{
                                            tran.Name
                                        }}</p>

                                <p class=" text-center w-full font-[600] text-[12px] text-[#64748b] ">{{ tran.Sku }}</p>
                                <p class=" text-center w-full font-[600] text-[12px] text-[#64748b]">{{ tran.Category }}
                                </p>
                                <p class=" text-center w-full font-[600] text-[12px] text-[#64748b]">$ <span
                                        class="text-[14px] text-black">{{ tran.Price }}</span>
                                </p>
                                <p class=" text-center w-full font-[600] text-[12px] text-[#64748b]"> <span
                                        class="text-[14px] text-black">{{ tran.Quantity }}</span>
                                    units</p>

                            </div>

                        </div>

                        <div class="flex justify-end gap-3 pt-2">
                            <button type="button" @click="cancelmt"
                                class="rounded-xl border border-slate-200 px-4 py-2.5 font-semibold hover:bg-slate-50 cursor-pointer">Cancel</button>
                            <button @click="sendToTransactions(tran.Price, tran.Name, tran.Icon, tran.Quantity)"
                                class="rounded-xl bg-emerald-600 px-5 py-2.5 font-semibold text-white hover:bg-emerald-700 cursor-pointer">
                                Send </button>
                        </div>
                    </div>
                </div>


            </div>
        </div>
    </section>
</template>
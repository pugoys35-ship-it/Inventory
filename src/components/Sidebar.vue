<!-- SIDEBAR -->
<script>


export default {
    emits: ['goTo', 'open', 'page', 'Inventory', 'prices', 'quantities', 'Units'],
    props: ['sidebarPage'],
    data() {
        return {
            modal: false,
            productName: '',
            sku: '',
            category: '',
            price: 0,
            quantity: 0,
            icon: '',
        }
    },
    methods: {
        navi(i) {
            this.$emit('goTo', i)
            console.log(this.productName)
        },

        openModal() {
            this.modal = true;
        },

        closeModal() {
            this.modal = false;
        },

        addProduct() {
            if (this.productName !== '' && this.sku !== '' && this.category !== '' && this.price !== 0 && this.quantity !== 0 && this.icon !== '') {
                this.$emit('quantities', this.quantity)
                this.$emit('prices', this.price)
                this.$emit('open', { Name: this.productName, Sku: this.sku, Category: this.category, Price: this.price, Quantity: this.quantity, Icon: this.icon })
                alert("Successfully added to inventory!")
                this.modal = false;
                this.productName = '';
                this.sku = '';
                this.category = '';
                this.price = 0;
                this.quantity = 0;
                this.icon = '';
                this.$emit('page', 'Inventory')
            }

            else {
                alert('Fill up the remaining details of this product');
            }


        }
    }
}
</script>

<template>


    <!-- sidebar -->
    <nav class="">
        <div class="fixed w-[256px] z-999 bg-white border border-gray-400 h-screen flex flex-col justify-between  py-7  px-6">
            <div>
                <div class="flex gap-3">
                    <div
                        class=" w-[40px] h-[40px] rounded-[12px] bg-[#4f46e5] text-center flex justify-center text-white font-[700] text-[18px] items-center">
                        S
                    </div>
                    <div class="flex flex-col">
                        <div class="">
                            <p class="text-[18px] font-[700]">Stockly</p>
                        </div>
                        <div>
                            <p class="text-[12px] text-[#64748b]">Inventory Manager</p>
                        </div>
                    </div>
                </div>

                <div class="mt-10">
                    <p class="text-[#94a3b8] font-[600] text-[12px]">WORKSPACE</p>
                    <div class="mt-3">
                        <div @click="navi('Dashboard')"
                            class="cursor-pointer w-[207px] h-[48px] hover:bg-[#eef2ff] px-5 flex items-center rounded-xl text-[#4338ca] gap-3 font-[600]">
                            <p>▦</p>
                            <p>Dashboard</p>
                        </div>
                        <div @click="navi('Inventory')"
                            class="cursor-pointer w-[207px] h-[48px] hover:bg-[#eef2ff] px-5 flex items-center rounded-xl text-[#4338ca] gap-3 font-[600]">
                            <p>▤</p>
                            <p>Inventory</p>
                        </div>
                        <div @click="navi('Transactions')"
                            class="cursor-pointer w-[207px] h-[48px] hover:bg-[#eef2ff] px-5 flex items-center rounded-xl text-[#4338ca] gap-3 font-[600]">
                            <p>❒</p>
                            <p>Transactions</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="w-[217.2px] h-[124px] bg-[#0f172a] rounded-xl px-5 py-4 animate-pulse">
                <p class="font-[600] text-white">Keep stock in check</p>
                <p class="text-[14px] text-[#cbd5e1]">Track your products, <br> quantities, and stocks, <br> in
                    one place</p>
            </div>
        </div>
    </nav>
    <nav
        class="fixed w-full h-[84.8px] bg-white/90 backdrop-blur-md z-99 border border-gray-400 flex justify-between items-center px-10">
        <div class="ml-62">
            <p class="text-[#64748b] text-[14px]">Workspace / Overview</p>
            <p class="text-[24px] font-[700]">Inventory Dashboard</p>
        </div>
        <button @click="openModal"
            class="px-6 py-3 hover:bg-[#4f46e5]/80 duration-300 hover:scale-101 rounded-xl bg-[#4f46e5] text-[14px] font-[600] text-white">+
            Add product</button>
    </nav>

    <!--add product modal -->
    <div v-if="modal" class="z-20 bg-black/30 fixed w-full h-screen flex justify-center items-center">
        <div class="h-[527.2px] w-[512px] bg-white rounded-xl px-5 py-6 space-y-3">
            <div>
                <h1 class="font-[700] text-[#1e293b] text-[20px]">Add new product</h1>
                <p class="text-[#64748b] text-[14px]">Enter the product information below.</p>
            </div>
            <div>
                <p></p>
            </div>
            <div>
                <h1 class="font-semibold mb-1.5 text-sm">Product name *</h1>
                <input v-model="productName" maxlength="80" placeholder="Type a product name"
                    class="w-full rounded-xl border border-slate-200 px-3 py-2.5 outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-100 cursor-pointer">
            </div>
            <div class="flex gap-2 ">
                <div class="w-full">
                    <h1 class="font-semibold mb-1.5 text-sm">SKU *</h1>
                    <input v-model="sku" maxlength="30" placeholder="Code for your product"
                        class="w-full rounded-xl border border-slate-200 px-3 py-2.5 outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-100 cursor-pointer">
                </div>
                <div class="w-full">
                    <h1 class="font-semibold mb-1.5 text-sm">Category</h1>
                    <select v-model="category"
                        class="w-full rounded-xl border border-slate-200 px-3 py-2.5 outline-none focus:border-indigo-500 cursor-pointer">
                        <option>Smart Phone</option>
                        <option>Tablet</option>
                        <option>Laptop</option>
                        <option>PC</option>
                        <option>Accesories</option>


                    </select>
                </div>
            </div>
            <div class="flex gap-2 ">
                <div class="w-full">
                    <h1 class="font-semibold mb-1.5 text-sm">Price *</h1>
                    <input v-model="price" maxlength="30" type="number" placeholder="0"
                        class="w-full rounded-xl border border-slate-200 px-3 py-2.5 outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-100 cursor-pointer">
                </div>
                <div class="w-full">
                    <h1 class="font-semibold mb-1.5 text-sm">Quantity *</h1>
                    <input v-model="quantity" maxlength="30" type="number" placeholder="0"
                        class="w-full rounded-xl border border-slate-200 px-3 py-2.5 outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-100 cursor-pointer">
                </div>
            </div>
            <div>
                <h1 class="font-semibold mb-1.5 text-sm">Icon</h1>
                <select v-model="icon"
                    class="w-full rounded-xl border border-slate-200 px-3 py-2.5 outline-none focus:border-indigo-500 cursor-pointer">
                    <option>📱</option>
                    <option>🔳</option>
                    <option>💻</option>
                    <option>🖥️</option>
                    <option>🎮</option>
                </select>
            </div>
            <div class="flex justify-end gap-3 pt-2">
                <button type="button" @click="closeModal"
                    class="rounded-xl border border-slate-200 px-4 py-2.5 font-semibold hover:bg-slate-50 cursor-pointer">Cancel</button>
                <button @click="addProduct"
                    class="rounded-xl bg-indigo-600 px-5 py-2.5 font-semibold text-white hover:bg-indigo-700 cursor-pointer">
                    Add product </button>
            </div>
        </div>
    </div>
</template>
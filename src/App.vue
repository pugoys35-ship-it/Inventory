  <!-- app -->

  <script>
  import Dashboard from './components/Dashboard.vue'
  import Sidebar from './components/Sidebar.vue'
  import Inventory from './components/Inventory.vue'
  import Transactions from './components/Transactions.vue';
  import Footer from './components/Footer.vue';

  export default {
    components: {
      Dashboard,
      Sidebar,
      Transactions,
      Inventory,
      Footer
    },
    data() {
      return {
        currentPage: 'Dashboard',
        inventory: [],
        transactions: [],
        realtrans: [],
        priceNum: 0,
        quantityNum: 0,
        Units: 0,
        userRname: '',
        propertyName: 'User',
      }
    },
    methods: {
      navi(i) {
        this.currentPage = i;
      },
      to(product) {
        this.inventory.push(product);
      },

      length() {
        this.units = this.inventory.length
      },

      price(p) {
        this.priceNum += p;
      },

      quantity(q) {
        this.quantityNum += q;

      },
      minusan(i) {
        this.priceNum -= i;
      },
      minusanQ(a) {
        this.quantityNum -= a;
      },
      minustranprice(i) {
        this.priceNum -= i;
      },
      minustranquan(i) {
        this.quantityNum -= i;
      },
      pushTotrans(t) {
        this.transactions.push(t)
      },
      addtoTran(receiverN, price, name, icon, quantity) {
        this.realtrans.push({ ...receiverN, ...price, ...name, ...icon, ...quantity });
      },
      username(u) {
        this.userRname = u;
      }
    }

  }

</script>

  <template>
    <Sidebar @goTo="navi" @open="to" @page="navi" @prices="price" @quantities="quantity" @units="length"
      :sidebarPage="currentPage" />
    <Dashboard v-if="currentPage === 'Dashboard'" :myInventory=inventory :totalPrice=priceNum :totalQuantity=quantityNum
      :totalUnit="Units" />
    <Transactions v-if="currentPage === 'Transactions'" :user="userRname" :tranArray="realtrans" :myt="realtrans" />
    <Inventory v-if="currentPage === 'Inventory'" :myInventory=inventory @minus="minusan" @minusQ="minusanQ"
      @minusTran="minustranprice" @minusTranQ="minustranquan" @addTotrans="pushTotrans" @goTran="addtoTran"
      @rName="username" @gotranSec="navi" />
    <Footer />
  </template>
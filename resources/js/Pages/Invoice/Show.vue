<template>
    <div class="container">
        <div class="invoices">
        
            <!-- <div class="card__header not_for_print">
                <div>
                    <h2 class="invoice__title">Invoice</h2>
                </div>
            </div> -->
            <div class="not_for_print">
                <!-- <div class="card__header--title ">
                    <h1 class="mr-2">#{{props.invoice.number}}</h1>
                    <p>{{props.invoice.created_at}} </p>
                </div> -->
        
                <div>
                    <ul  class="card__header-list">
                        <li>
                            <button class="flex justify-center px-4 mr-3 border border-slate-800 rounded-lg text-black" @click.prevent="print">
                                <i class="fas fa-print"></i>
                                Print
                            </button>
                        </li>
                        <li>
                            <Link :href="route('invoice.edit', props.invoice)" class="flex justify-center px-4 mr-3 border border-slate-800 rounded-lg text-black">
                                <i class=" fas fa-reply"></i>
                                Edit
                            </Link>

                        </li>
                        <li>
                            <Link :href="route('invoice.index')" class="flex justify-center px-4 mr-3 border border-slate-800 rounded-lg text-black">
                                <i class=" fas fa-pencil-alt"></i>
                                Inapoi
                            </Link>
                        </li>
                        
                    </ul>
                </div>
            </div>

            <div class="table invoice">
                <!-- <div class="logo">
                    <img src="assets/img/logo.png" alt="" style="width: 200px;">
                </div> -->
                <div class="invoice__header--title">
                    <p></p>
                    <p class="invoice__header--title-1">Invoice</p>
                    <p></p>
                </div>

                
                <div class="invoice__header--item">
                    <div>
                        <h2>Invoice To:</h2>
                        <p>{{props.invoice.customer.name}}</p>
                    </div>
                    <div>
                            <div class="invoice__header--item1">
                                <p>Invoice#</p>
                                <span>#{{props.invoice.number}}</span>
                            </div>
                            <div class="invoice__header--item2">
                                <p>Date</p>
                                <span>{{props.invoice.date}}</span>
                            </div>
                            <div class="invoice__header--item2">
                                <p>Due Date</p>
                                <span>{{props.invoice.due_date}}</span>
                            </div>
                            <div class="invoice__header--item2">
                                <p>Reference</p>
                                <span>{{props.invoice.reference}}</span>
                            </div>
                        
                    </div>
                </div>

                <div class="table py1">

                    <div class="table--heading3">
                        <p>#</p>
                        <p>Item Description</p>
                        <p>Unit Price</p>
                        <p>Qty</p>
                        <p>Total</p>
                    </div>
        
                    <!-- item 1 -->
                    <div class="table--items3" v-for="(item, index) in props.invoice.products" :key="item.id">
                        <p>{{index + 1}}</p>
                        <p>{{item.name}}</p>
                        <p>$ {{item.price}}</p>
                        <p>{{item.pivot.quantity}}</p>
                        <p>$ {{item.price * item.pivot.quantity}}</p>
                    </div>
                </div>

                <div  class="invoice__subtotal">
                    <div>
                        <h2>Thank you for your business</h2>   
                    </div>
                    <div>
                        <div class="invoice__subtotal--item1">
                            <p>Sub Total</p>
                            <span> $ {{props.invoice.sub_total}}</span>
                        </div>
                        <div class="invoice__subtotal--item2">
                            <p>Discount</p>
                            <span>$ {{props.invoice.discount}}</span>
                        </div>
                        
                    </div>
                </div>

                <div class="invoice__total">
                    <div>
                        <h2>Terms and Conditions</h2>
                        <p>{{props.invoice.terms_and_conditions}}</p>
                    </div>
                    <div>
                        <div class="grand__total" >
                            <div class="grand__total--items">
                                <p>Grand Total</p>
                                <span>$ {{props.invoice.total}}</span>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
           
        </div>
    </div>
</template>

<script setup>
import { router, Link } from '@inertiajs/vue3';

const props = defineProps({
    invoice: {
        type: Object,
        required: true,
    }
})

const print = () => {
    window.print()
    router.push('/').catch(()=> {})
}
</script>


<style scoped>
@media print{
.not_for_print {
    display: none;
}
}

</style>
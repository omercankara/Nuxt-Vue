<template>
            <section class="bg-gray-900 w-1/3 mx-auto mt-10 p-2 px-5 rounded-md shadow-2xl">
      <!-- FAtura Bilgileri -->
      
     <contactSection  :contact="state.contact"/>
    

      <div class="mt-5">
        <heading title="Fatura Kalemleri"/>
        <invoiceitems  :items="state.items"  :AddInvoiceItem="AddInvoiceItem" />
      </div>

      <!-- Summary -->
        <invoicesummary :items = "state.items"   />

      <hr class="bg-gradient-to-r h-[1px] border-none from-gray-700 mt-5" />
      <div class="actionbar text-right my-5">
        <button @click="onSubmit" class="purple-button">Kaydet</button>
      </div>
    </section>
</template>

<script setup>
//yeni data dağıtımı bu component uzerınden olcak
         import invoiceitems from  "./invoiceItems.vue"
         import invoicesummary from "./invoicesummary.vue"
         import contactSection from "./contactSection.vue"
         import {reactive,provide,watch} from "vue"

const props  = defineProps({saveInvoce:Function,  activeInvoice : [Object,null] })

//Müşteri dataları burada tut
const state = reactive({
        contact:{
                contact_name:null,
                email:null,
                city:null,
                country:null,
                zipcode:null,
        },
        items:[]
})

const AddInvoiceItem = () => {
        state.items.push({
                id:new  Date().getTime(),
                name:null,
                qty:null,
                unit_price:0,
                total_price:0.0
        })
        console.log(state.items)
}

const DeleteInvoiceItem = (invoiceItem) => {
        state.items = state.items.filter(i=>i.id !== invoiceItem.id)
}

const onSubmit = () => {

        props.saveInvoce({...state, createAt: new Date(), id:new Date().getTime() }) //state içindeki elemanları da aktar
        //girildikten sonra inputları temizle
        state.contact = {
                contact_name:null,
                email:null,
                city:null,
                country:null,
                zipcode:null,
        }
        state.items = []
};

console.log("Active İnvoices",  props.activeInvoice)

watch(() =>props.activeInvoice, (activeInvoice)=> {
        console.log("Active İnvoices", activeInvoice)
        if(activeInvoice){ //varsa
                state.contact = {
                        ...activeInvoice.contact
                }
                state.items = [...activeInvoice.items]
        }
})
 
provide("DeleteInvoiceItem", DeleteInvoiceItem ) // fonksiyonu gonder
</script>
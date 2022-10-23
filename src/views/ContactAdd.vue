<template>
    <div v-if="contact" class="page">
        <h4>Thêm liên hệ</h4>
        <ContactForm
            :contact="contact"
            @submit:contact="addNewContact"
        />
        <p>{{message}}</p>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";
export default {
    components:{
        ContactForm,
    },
    data(){
        return{
            contact: null,
            message: "",
        };
    },
    methods:{
        async addNewContact(data){
            try {
                await ContactService.create(data);
                this.message = "Liên hệ mới được thêm thành công.";
            } catch (error) {
                console.log(error);
            }
        },
    },
    created(){
        this.contact = new Object();
        this.message = "";
    },
}
</script>
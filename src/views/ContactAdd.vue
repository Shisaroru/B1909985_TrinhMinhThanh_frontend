<template>
    <div class="page">
        <h4>Thêm liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="addContact"></ContactForm>
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from '../components/ContactForm.vue';
import ContactService from '@/services/contact.service';

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: null,
            message: "",
        }
    },
    methods: {
        async addContact(data) {
            try {
                await ContactService.create(data)
                this.message = "Liên hệ được tạo thành công"
            } catch (error) {
                console.log(error);
            }
        },
    },
    created() {
        this.contact = {}
        this.message = ""
    }
}
</script>
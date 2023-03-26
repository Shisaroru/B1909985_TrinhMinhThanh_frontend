<template>
    <Form @submit="submitContact" :validation-schema="contactFormSchema">
        <div class="form-group">
            <label for="name">Tên</label>
            <Field name="name" class="form-control" type="text" v-model="contactLocal.name"/>
            <ErrorMessage name="name" class="error-feedback"/>
        </div>
        <div class="form-group">
            <label for="email">Email</label>
            <Field name="email" class="form-control" type="email" v-model="contactLocal.email"/>
            <ErrorMessage name="email" class="error-feedback"/>
        </div>
        <div class="form-group">
            <label for="address">Địa chỉ</label>
            <Field name="address" class="form-control" type="text" v-model="contactLocal.address"/>
            <ErrorMessage name="address" class="error-feedback"/>
        </div>
        <div class="form-group">
            <label for="phone">Điện thoại</label>
            <Field name="phone" class="form-control" type="tel" v-model="contactLocal.phone"/>
            <ErrorMessage name="phone" class="error-feedback"/>
        </div>
        <div class="form-group">
            <label for="address">Địa chỉ</label>
            <Field name="address" class="form-control" type="text" v-model="contactLocal.address"/>
            <ErrorMessage name="address" class="error-feedback"/>
        </div>
        <div class="form-group">
            <label for="phone">Điện thoại</label>
            <Field name="phone" class="form-control" type="tel" v-model="contactLocal.phone"/>
            <ErrorMessage name="phone" class="error-feedback"/>
        </div>
        <div class="form-group form-check">
            <input type="checkbox" name="favorite" v-model="contactLocal.favorite" class="form-check-input"/>
            <label for="favorite" class="form-check-label">
                <strong>Liên hệ yêu thích</strong>
            </label>
        </div>
        <div class="form-group">
            <button class="btn btn-primary">Lưu</button>
            <button class="ml-2 btn btn-danger" type="button" v-if="contactLocal._id" @click="deleteContact">Xóa</button>
        </div>
    </Form>
</template>

<script>
import * as yup from "yup"
import { Form, Field, ErrorMessage } from "vee-validate"

export default {
    components: {
        Form,
        Field,
        ErrorMessage,
    },
    emits: ["submit:contact", "delete:contact"],
    props: {
        contact: { type: Object, required: true,}
    },
    data() {
        const contactFormSchema = yup.object().shape({
            name: yup.string().required("Tên phải có giá trị").min(2,"Tên phải ít nhất có 2 ký tự").max(50, "Email tối đa 50 ký tự"),
            email: yup.string().email("Email không đúng").max(50, "Email tối đa 50 ký tự"),
            address: yup.string().max(100, "Địa chỉ tối đa 100 ký tự"),
            phone: yup.string().matches(/((09|03|07|08|05)+([0-9]{8})\b)/g, "Số điện thoại không hợp lệ"),
        })
        return {
            // Chúng ta sẽ không muốn hiệu chỉnh props, nên tạo biến cục bộ
            // contactLocal để liên kết với các input trên form
            contactLocal: this.contact,
            contactFormSchema,
        }
    },
    methods: {
        submitContact() {
            this.$emit("submit:contact", this.contactLocal)
        },
        deleteContact() {
            this.$emit("delete:contact", this.contactLocal.id)
        },
    }
}
</script>

<style scoped>
@import "@/assets/form.css";
</style>
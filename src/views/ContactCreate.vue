<template>
    <div class="page">
        <h4>Tạo mới Liên hệ</h4>
        <!-- Sử dụng ContactForm, không cần truyền prop contact vì đây là tạo mới -->
        <ContactForm :contact="contact" @submit:contact="createContact" />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: {
                name: "",
                email: "",
                address: "",
                phone: "",
                favorite: false,
            },
            message: "",
        };
    },
    methods: {
        async createContact(data) {
            try {
                // Gửi yêu cầu POST đến API để tạo liên hệ mới
                await ContactService.create(data);
                // Hiển thị thông báo thành công
                alert('Liên hệ được tạo thành công.');
                // Chuyển hướng về trang contactbook sau khi tạo thành công
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log(error);
                this.message = 'Đã xảy ra lỗi khi tạo liên hệ.';
            }
        },
    },
};
</script>

<style scoped>
@import "@/assets/form.css";
</style>

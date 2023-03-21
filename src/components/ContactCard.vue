<script>
export default {
    props: {
        contact: {type: Object, required: true},
    },
}
</script>

<template>
    <div>
        <div class="p-1">
            <strong>
                Tên:
            </strong>
            {{ contact.name }}
        </div>
        <div class="p-1">
            <strong>
                Email:
            </strong>
            {{ contact.email }}
        </div>
        <div class="p-1">
            <strong>
                Địa chỉ:
            </strong>
            {{ contact.address }}
        </div>
        <div class="p-1">
            <strong>
                Điện thoại:
            </strong>
            {{ contact.phone }}
        </div>
        <div class="p-1">
            <strong>
                Liên hệ yêu thích:&nbsp;
            </strong>
            <i v-if="contact.favorite" class="fas fa-check"></i>
            <i class="fas fa-times" v-else></i>
        </div>
    </div>
</template>
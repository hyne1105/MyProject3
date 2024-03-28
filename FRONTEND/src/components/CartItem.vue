<script>
export default {
    data() {
        return {
            products: [],
        }
    },
    props: {
        refeshlistcart: Function,
        carts: Array,
    },
    emit: [
        "deleted:cartIndex"
    ],
    methods: {
        deletedcart(index) {
            this.$emit("deleted:cartIndex", index);
        },
    },
}
</script>
<template>
    <div class="row mb-4 align-items-center" v-for="(item, index) in carts">
        <div class="col-md-2">
            <img :src="item.img" class="img-fluid">
        </div>
        <div class="col-md-4">
            <h6>{{ item.title }}</h6>
            <div>
                <span>Kích thước: <span>{{ item.size }}</span></span>
                <br>
                <span>Màu chậu: <span>{{ item.color }}</span></span>
                <br>
                <span>Số lượng: <span>{{ item.quantity }}</span></span>
            </div>
        </div>
        <div class="col-md-3" @click="deletedcart(index)">
            <button class="button4">
                <svg viewBox="0 0 448 512" class="svgIcon">
                    <path
                        d="M135.2 17.7L128 32H32C14.3 32 0 46.3 0 64S14.3 96 32 96H416c17.7 0 32-14.3 32-32s-14.3-32-32-32H320l-7.2-14.3C307.4 6.8 296.3 0 284.2 0H163.8c-12.1 0-23.2 6.8-28.6 17.7zM416 128H32L53.2 467c1.6 25.3 22.6 45 47.9 45H346.9c25.3 0 46.3-19.7 47.9-45L416 128z">
                    </path>
                </svg>
            </button>
        </div>
        <div class="col-md-3 text-center">
            <h6 class="mb-0 price">{{ (item.price * item.quantity).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".") }} VNĐ</h6>
        </div>
    </div>
    <hr>
</template>
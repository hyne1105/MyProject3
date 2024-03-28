<script>
export default {
    props: {
        products: { type: Object, required: true },
    },
};
</script>
<template>
    <div class="card1">
        <div class="infos">
            <div class="image1"><img :src="products.img[0]" alt="img" width="100"></div>
            <div class="info">
                <div>
                    <p class="name">
                        {{ products.title }}
                    </p>
                    <p class="function">
                        {{ products.price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".") }} VNĐ
                    </p>
                    <p class="function">
                        {{ products.desc }}
                    </p>
                </div>
            </div>
        </div>
        <!-- <button class="request" type="button">
            Add friend
        </button> -->
    </div>
</template>

<style scoped>
.card1 {
    min-width: 300px;
    min-height: 400px;
    border-radius: 1rem;
    background-color: rgba(31, 41, 55, 1);
    padding: 1rem;
    box-shadow: 10px 10px 5px rgba(0, 0, 0, 0.376);
}

.infos {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    grid-gap: 1rem;
    gap: 1rem;
}

.image1 {
    height: 5rem;
    width: 5rem;
    border-radius: 0.5rem;
    background-color: rgb(118, 36, 194);
    background: linear-gradient(to bottom right, rgb(118, 36, 194), rgb(185, 128, 240));
}

.info {
    padding-left: 40px;
    height: 7rem;
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.name {
    font-size: 1.25rem;
    line-height: 1.75rem;
    font-weight: 500;
    color: rgba(255, 255, 255, 1);
}

.function {
    font-size: 0.75rem;
    line-height: 1rem;
    color: rgba(156, 163, 175, 1);
}

.stats {
    width: 100%;
    border-radius: 0.5rem;
    background-color: rgba(255, 255, 255, 1);
    padding: 0.5rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 0.75rem;
    line-height: 1rem;
    color: rgba(0, 0, 0, 1);
}

.flex {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0 4px;
}

.state-value {
    font-weight: 700;
    color: rgb(118, 36, 194);
}

.request {
    margin-top: 1.5rem;
    width: 100%;
    border: 1px solid transparent;
    border-radius: 0.5rem;
    padding: 0.5rem 1rem;
    font-size: 1rem;
    line-height: 1.5rem;
    transition: all .3s ease;
}

.request:hover {
    background-color: rgb(118, 36, 194);
    color: #fff;
}
</style>

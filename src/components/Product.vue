<template>
    <div class="card my-5">
        <div class="card-body">
            <h5 class="text-center card-title">{{product.employee_name}}</h5>
            <p class="text-center text-muted card-text display-4">${{product.employee_salary}}</p>
            <button :disabled="isInCart" @click="$emit('add-to-cart',product)" class="btn btn-info form-control">
                {{isInCart ? 'Added to cart': 'Add to Cart'}}
            </button>
        </div>
    </div>
</template>

<script>
export default{
    props: ['product','isInCart']
}
</script>

<template>
                
                <div class="card">
                    <div class="card-header bg-primary text-light">
                        <i class="fas fas-comments"></i> Chat Box
                        </div>
                    <div class="card-body">
                        <div>
                            <chat-message-component/>
                            <chat-form-component/>
                        </div>
                    </div>
                </div>
</template>

<script>
    export default {
        mounted() {
            // console.log('Component mounted.')
        }
    }
</script>
